
# 논문 정리

# 공동저자: 언어 모델 기능 탐색을 위한 인간-AI ​​공동 쓰기 데이터세트 설계

Mina Lee minalee@cs.stanford.edu Stanford University United States 
Percy Liang pliang@cs.stanford.edu Stanford University United States 
Qian Yang qianyang@cornell.edu Cornell University United States

이 문서에서는 창의적이고 논쟁적인 글쓰기를 지원하는 능력을 더 잘 이해하기 위해 GPT-3와 같은 대규모 언어 모델을 상호 작용 데이터 세트를 통해 분석할 수 있는 방법에 대해 논의합니다. 저자는 작가와 GPT-3 간의 상호 작용을 캡처하여 언어, 아이디어 및 협업 능력을 탐색하는 CoAuthor라는 데이터 세트를 소개합니다. 이는 상호 작용 디자인에서 이러한 모델을 사용할 때의 잠재적인 이점과 과제에 대한 보다 정보에 기반한 토론을 촉진하는 것을 목표로 합니다.

## 페이지 1

- •이 논문에서는 특히 인간-컴퓨터 상호 작용(HCI)의 맥락에서 언어 모델의 생성 기능을 더 잘 이해하기 위해 대규모 상호 작용 데이터 세트를 관리하고 분석하는 것의 중요성에 대해 논의합니다.
- •CoAuthor라는 데이터 세트는 작성자와 GPT-3 인스턴스 간의 상호 작용을 캡처하여 창의적이고 논쟁적인 글쓰기를 지원하는 GPT-3의 능력을 탐색하기 위한 도구로 도입되었습니다.
- •연구자들은 이전 텍스트나 디코딩 매개변수와 같은 요소를 기반으로 LM의 성능 변동성을 조사함으로써 이러한 모델이 글쓰기 작업에 어떻게 기여하는지에 대한 통찰력을 얻을 수 있습니다.

## 페이지 2

- •본문에서는 고갈된 우라늄으로 집을 짓는 작은 돼지에 대해 이야기합니다. 그 집이 자신을 독살할 것이라는 것을 알고 대신 숨겨진 오두막에서 살기로 결정했습니다.
- •CoAuthor라는 데이터 세트는 대화형 쓰기를 위한 GPT-3의 생성 기능을 공개하고 여러 세션에 걸쳐 작가와 GPT-3 인스턴스 간의 상호 작용을 보여주기 위해 도입되었습니다.
- •이 논문은 상호 작용 디자인에서 언어 모델의 생성 기능을 이해해야 할 필요성을 강조하고, 이러한 기능에 더 쉽게 접근할 수 있도록 하는 접근 방식으로 대규모 상호 작용 데이터 세트를 제안합니다.

## 페이지 3

- •엄청난 양의 텍스트에 대해 훈련된 언어 모델(LM)은 결함이 있거나 부정확하거나 윤리적으로 문제가 있는 텍스트를 생성할 수 있습니다.
- •대화형 글쓰기를 위한 LM의 생성 능력을 이해하는 것은 상황 의존성과 주관적 해석으로 인해 어렵습니다.
- •인간-컴퓨터 상호작용(HCI) 연구의 전통적인 방법은 LM의 생성 능력을 조사할 때 한계가 있습니다. 로깅 상호 작용과 같은 새로운 접근 방식이 등장하고 있습니다.

## 4 페이지

- •기술은 사람들을 만나고, 소통하고, 직접 만나기 전에 알아가는 것을 더 쉽게 만들어 데이트에 긍정적인 영향을 미쳤습니다.
- •이 텍스트에서는 대화형 글쓰기에서 언어 모델의 생성 기능을 이해하기 위한 CoAuthor라는 데이터 세트의 설계에 대해 설명합니다. 이는 다양한 맥락을 다루고, 주관적인 해석을 지원하고, 결과뿐만 아니라 프로세스를 포착하고, 재사용 및 확장 가능성을 허용하는 것을 강조합니다.
- •CoAuthor 데이터 세트에는 다양한 글쓰기 작업(창의적 글쓰기 및 논증적 글쓰기), 다양한 프롬프트 소스(예: Writing-Prompts 하위 레딧 및 The New York Times)에 걸친 작가와 언어 모델 간의 상호 작용은 물론 잠재적으로 다른 배경을 가진 63명의 크라우드 작업자가 포함됩니다.

## 5 페이지

- •이벤트: 이벤트는 텍스트 삽입 또는 삭제, 커서 앞뒤로 이동, 시스템에서 제안 받기, 제안 수락/해제 등이 될 수 있습니다. 이벤트의 세부 사항은 표 1에 나열되어 있습니다.
- •이벤트 블록: 기록된 이벤트는 추가 처리 및 분석을 위해 결정적이고 중복되지 않는 이벤트 블록으로 추상화됩니다. 모든 이벤트 블록은 표 2에 나와 있습니다.
- •CoAuthor 디자인: 데이터 세트는 텍스트 편집기와 유사한 모델 독립적인 사용자 인터페이스를 사용하여 향후 다양한 쓰기 작업을 위해 재사용하고 쉽게 확장할 수 있도록 설계되었습니다.

## 6 페이지

- •시스템의 사용자 인터페이스와 상호 작용 디자인은 Write With Transformer 및 Buschek et al.과 같은 관련 디자인의 영향을 받았습니다.
- •CoAuthor의 데이터 세트에는 창의적 글쓰기를 위해 58명의 작가가 쓴 830개의 이야기와 49명의 논증적 글쓰기를 위한 615개의 에세이가 포함되어 있으며 각 세션의 평균은 418단어의 텍스트로 구성됩니다.
- •CoAuthor는 언어 능력, 아이디어 능력, 협업 능력에 중점을 두고 창의적이고 논쟁적인 글쓰기를 지원하는 GPT-3의 생성 능력을 입증하는 데 사용되었습니다.

## 7 페이지

- •CoAuthor 데이터세트는 창의적이고 논쟁적인 글쓰기의 글쓰기 세션으로 구성되며, 63명의 작가가 1445개의 세션을 작성했습니다.
- •GPT-3에서 생성된 문장은 인간 작가가 작성한 문장에 비해 철자 및 문법 오류가 적었습니다.
- •GPT-3을 사용한 공동 작문은 인간이나 AI가 단독으로 작성한 텍스트에 비해 어휘 사용이 더 다양해졌습니다.

## 페이지 8

- •자신도 모르게 같은 변신술사와 데이트를 계속해온 한 여성은 이번에는 ER의 조지 클루니를 닮은 매력적인 의사로 변신해 이를 해결하기로 결심한다.
- •Jim이라는 변신술사는 전략적으로 여성 Karen이 그녀의 마음을 사로잡기 위해 천식 치료를 받는 의료 센터에 일자리를 얻습니다.
- •설문 조사 응답은 AI 제안에 대한 작가의 다양한 반응을 나타냅니다. 어떤 사람들은 그것이 도움이 되고 영감을 준다고 생각하는 반면 다른 사람들은 수정이 필요한 문법 오류를 지적합니다.

## 페이지 9

- •무작위성이 높은 GPT-3는 무작위성이 낮은 것에 비해 새로운 명명된 엔터티로 문장을 생성할 가능성이 더 높았습니다.
- •공동 작업의 평등과 상호성은 작가에 따라 크게 다르지만 프롬프트에서는 덜 다릅니다.
- •무작위성이 높은 GPT-3를 사용한 글쓰기 세션은 논증적 글쓰기에서 약간 더 높은 평등성 및 상호성 점수를 받았습니다.

## 페이지 10

- •이 연구는 공동 작문 시나리오에서 작가의 생산성과 주인의식에 대한 GPT-3의 영향을 탐구합니다.
- •텍스트 생성 증가와 긍정적인 상관관계가 있는 요인에는 작성에 소요된 시간, 쿼리 수, GPT-3에서 허용된 제안 등이 있습니다.
- •GPT-3를 사용할 때 작가가 작성한 텍스트의 비율과 최종 텍스트에 대한 소유권 사이에는 상관 관계가 있습니다.

## 페이지 11

- •CHI '22에서 제시된 CoAuthor 데이터 세트를 통해 HCI 및 NLP 커뮤니티는 언어 모델의 생성 기능을 이해할 수 있습니다.
- •연구원은 CoAuthor를 사용하여 가설을 공식화하고 타당성을 평가하며 대화형 글쓰기를 위한 언어 모델을 훈련/평가할 수 있습니다.
- •이 데이터세트에는 1,445개의 글쓰기 세션에서 작가와 GPT-3 간의 상호 작용이 포함되어 있어 상호 작용 디자인 연구에 귀중한 통찰력을 제공합니다.

## 페이지 12

- •이 텍스트에는 자연어 처리, 기계 학습 및 인간-컴퓨터 상호 작용과 관련된 다양한 학술 논문 및 컨퍼런스에 대한 참고 자료가 포함되어 있습니다.
- •이 분야의 연구에 기여한 Lee et al., Andrea Cuadra, Hansol Lee, Jason Cho, Wendy Ju와 같은 특정 저자를 언급합니다.
- •음악에서 실시간 대화형 기계 학습을 위한 Wekinator와 같은 도구와 기계 텍스트를 면밀히 조사하기 위한 Scarecrow와 같은 프레임워크에 대한 참조가 있습니다.

## 페이지 13

- •이 텍스트에는 인간-AI ​​공동 작문, NLP 벤치마킹, 차량-운전자 통신 타이밍, ESL 쌍 작업 상호 작용 패턴, 시각 장애인의 객체 인식을 위한 장애 우선 데이터 세트 생성과 관련된 다양한 연구 및 데이터 세트에 대한 참조가 포함되어 있습니다.
- •GPT-3에서 제안을 생성하기 위해 Flask를 사용하여 Python으로 작성된 서버에서 사용되는 시스템 설정과 이러한 제안이 가독성과 적절성을 기준으로 필터링되는 방법에 대한 세부 정보를 제공합니다.
- •창의적 글쓰기와 논증적 글쓰기에 사용되는 쓰기 프롬프트가 프롬프트별 작가 참여를 보여주는 데이터와 함께 제공됩니다.

## 페이지 14

- •한 여자가 자신도 모르게 같은 변신술사와 반복적으로 데이트를 한다.
- •사람들은 전생이 등장하는 영화관에서 죽은 뒤 큰 화면으로 다음 생을 지켜본다.
- •적대적인 외계인이 숫자를 줄이면 인류는 마법의 힘을 재발견합니다.

## 페이지 15

- •이 텍스트는 팬데믹 기간 중 화면 시청 시간, 기술이 데이트에 미치는 영향, 학교에서 무료 패드 및 탐폰 제공, 학생들이 학교에서 배워야 할 중요한 사항, 미디어 콘텐츠의 고정관념, 오디오북 듣기와 책 읽기 등 사회 문제와 관련된 다양한 프롬프트를 논의합니다.
- •또한 대학 운동선수에게 돈을 지불해야 하는지, 위험한 스포츠를 추구하는 것이 이기적인지 등 논란이 많은 주제를 다룹니다.
- •마지막으로, 인간의 고통보다 동물 복지에 초점을 맞추는 것에 의문을 제기하고 뉴스를 따라가며 책임감 있는 시민이 되는 것에 대해 토론합니다.

## 페이지 16

- •Lee et al. 시스템 요구 사항에 대한 이해를 입증하지 못하면 자동으로 실격 처리됩니다.
- •제출물 평가 기준: 스토리나 에세이의 명확한 결말, 명확한 입장 및 결론.
- •Amazon Mechanical Turk에서 사용된 지침은 창의적 글쓰기 자격 라운드와 논증적 글쓰기 메인 라운드에서 유사했습니다.

## 페이지 17

- •이 연구는 글쓰기 과정에서 인간과 AI 에이전트가 어떻게 협력하는지 이해하기 위해 공동 글쓰기에서 인간과 AI의 상호 작용에 관한 것입니다.
- •참가자는 AI가 생성한 다음 문장에 대한 제안과 함께 제공된 텍스트 편집기를 사용하여 스토리를 작성하라는 요청을 받게 되며, 이를 자신의 스토리에 통합할 수 있습니다.
- •연구와 관련된 위험에는 AI가 생성한 잠재적으로 공격적이거나 유발하는 콘텐츠가 포함되며 참가자는 식별 가능한 개인 정보를 공유하지 않는 것이 좋습니다.

## 18 페이지

- •참가자는 연구에 대한 우려 사항이나 불만 사항이 있는 경우 독립적인 출처에 문의할 수 있습니다.
- •목표는 AI 기반 작문 도우미의 도움을 받아 흥미로운 이야기를 쓰는 것입니다.
- •이 작업에는 AI와 협력하여 최소 10분 동안 스토리를 작성하고 스토리가 명확한 결말을 갖도록 해야 합니다.

## 페이지 19

- •이 텍스트는 미국 뉴올리언스에서 열린 CHI '22에서 발표된 인간-AI ​​공동 작문 데이터 세트와 관련이 있습니다.
- •AI와 공동으로 스토리 작성 및 인증 코드 입력과 관련된 설문 조사 작성 지침이 제공됩니다.
- •이 과정에는 스토리를 설문조사에 직접 입력하지 않고 복사하여 붙여넣는 과정이 포함됩니다.