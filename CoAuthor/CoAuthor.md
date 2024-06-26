
# 개요
### 프로그램 개요

- 본 논문에서는 생성형 인공지능을 활용한 작문 과정에서 **학습자와 인공지능의 작문 참여도를 시각화**여 보여줌으로써 나타나는 학습자의 행동을 분석하고자 합니다.
- 논문에 활용될 프로그램은 **선행연구에서 저자들이 공개한 프로그램들을 수정 및 조합하여 구성**할 예정이며, 현재 각 프로그램들은 **오픈 소스로 공개**되어 있습니다.
- 제가 활용할 선행연구 프로그램에 대한 **프로토타입, 설명**은 다음과 같습니다.

1. 프로그램 베이스는 Co-Author라는 생성형 인공지능 기반 작문 프로그램입니다(오른쪽 작문 인터페이스). 해당 프로그램의 인터페이스를 한국어로 바꾸고, 왼쪽에 학습자들이 작문 과정에서 인공지능의 제안을 얼마나 수용했는지 확인하기 위해 모니터링 프로그램을 구현하여 합쳐서 제작하고 싶습니다.
2. 모니터링 정보는 되도록 실시간으로 나타나야 합니다. 만약 실시간으로 반영되는 것이 어려울 경우 학습자가 (확인) 버튼을 누를 때마다 수정정보가 리뉴얼 될 수 있어야 합니다. 방법은 구현하기 쉬우신 방법으로 해주시되, 중점은 작문 과정에서 학습자가 모니터링을 볼 수 있도록 설계되어야 한다는 점입니다. 이 부분은 아마도 제가 제시해드리는 소스의 기본 로직을 바꿔야 할 것 같습니다.
3. 학습자가 입력하는 한 문장 단위로 인공지능 제안 정도가 나타나야하며, 작문 중 입력했던 문장을 수정하는 경우에도 이 부분이 반영되어야 합니다. 예를 들어 문장 7을 입력하는 중에 문장 4를 다시 수정하는 경우, 이 문장 4도 다시 시각화가 이루어져야 합니다. 또한 문장 6를 입력하다가 앞에 새로운 문장을 입력하거나 문장을 지우는 경우에도 바뀐 순서가 반영되어야 합니다.
4. Co-Author 프로그램 자체에 로그데이터를 수집할 수 있는 기능이 내장되어 있습니다. 또한 로그데이터를 기반으로 데이터를 판별할 수 있는 식 또한 이미 나와있습니다. 다만, 분류 프로그램의 기준이 영문 기반의 의미유사도 분류식이라 ‘GPT가 제안한 문장 의미 유사도 0.8 이상(이하)으로 수정’ 항목은 자연어 코드를 새롭게 짜야합니다. 새롭게 짠 자연어 코드는 추후 github으로 전달드릴 예정입니다.
5. 밑에 있는 색깔 설명은 인터페이스에 꼭 들어가지 않아도 괜찮습니다.


# 요구사항
- API
	- 기존 사용하던 text-davinci-003 모델 지원이 종료되어서 gpt-3.5-turbo-instruct 모델로 변경.
	- API 키 발급 필요.
	- GPT-3 모델을 기반으로 작성되었던 논문인 만큼 GPT-3.5 또는 GPT-4를 사용하여 실험 시 고려할 부분이 존재.
- 서버
	- 기존 소스 수정
		- 모델 변경 소스 적용
		- 한글 프롬프트 변경
			- blocklist.txt 한글화
				- 생성 AI 블랙리스트 설정 (욕설 등...)
			- prompt.tsv 한글화
				- 정확한 기능을 확인해야함.
		- 학습자들이 인공지능의 제안을 얼마나 수용했는지 모니터링 기능
			- 데이터 분석 프레임 적용
			- 학습자 로깅 수집 기능 추가
				- 로깅 분석 기능 필요.
			- 로깅 데이터 문장 유사도 계산 기능 추가
			- 기존 작문이 변경될 때 마다 반영
			- https://github.com/yixin-cheng/coAuthor 의 로그 수집 기능 서버에 적용
			- https://github.com/4N3MONE/nlp_tools 의 문장 유사도 계산 기능 서버에 적용
- 화면
	- 사이드 화면 추가
		- 사이드 화면에 문장 유사도를 서버로부터 받아와 수용한 문장을 기준으로 시각화 및 정렬
		- 기존 문장 수정 시 해당 문장 유사도 및 수정된 문장 반영 필요.


# 고려사항
- 기존 CoAuthor: Designing a Human-AI Collaborative Writing Dataset for Exploring Language Model Capabilities 의 논문에서는 GPT-3 모델을 사용함. 그러나 openAI 에서 GPT-3 모델의 지원이 종료되어 다른 모델을 채택해야함.
- 기존 논문에서 사용한 오픈소스에서는 신뢰성 있는 실험을 위해서 63명의 작가가 작성한 1445개의 데이터가 존재하였으나, 공유하지는 않았음. 즉, 한글로 작성된 신뢰성있는 데이터가 필요함.
- 로그 수집 기능 및 문장 유사도 기능을 실시간으로 적용하기를 원하는 경우에는 기존 오픈소스의 구성을 변경해야함. 기존 서버와 클라이언트를 http 소켓을 따로 띄워 API를 통해 기능을 통신하는 방식이었지만, 서버에 Jinaja2 템플릿 엔진을 통해 화면을 띄우면 네트워크 오버헤드가 줄어들어 효율적임.