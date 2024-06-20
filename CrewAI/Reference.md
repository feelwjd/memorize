
# 참조 자료들 모음


## GPT 모델 관련

- GPT 모델
	- gpt-4o
		- ![[Pasted image 20240620140757.png]]
		- 응답속도 제일 빠름
		- token 당 비용 비쌈
	- gpt-3.5-turbo
		- ![[Pasted image 20240620140828.png]]
- GPT 가격
	- https://openai.com/api/pricing/
	- Batch 사용 시 50% 저렴한 비용으로 사용 가능
		- https://platform.openai.com/docs/guides/batch
- open source model
	- hugging face에 openai의 gpt2 모델 공개 (2024-02)
		- https://huggingface.co/openai-community/gpt2
	- 레드파자마의 chat-3b-v1 모델
		- https://huggingface.co/togethercomputer/RedPajama-INCITE-Chat-3B-v1
	- 메타 Llama-3-8B-Instruct 모델 가장 괜찮아보임. (2024-05)
		- https://huggingface.co/meta-llama/Meta-Llama-3-8B-Instruct
		- CrewAI와 integration 내용
			- https://medium.com/@bhavikjikadara/step-by-step-guide-on-how-to-integrate-llama3-with-crewai-d9a49b48dbb2

---

## CrewAI
- 공식 문서
	- https://docs.crewai.com/
	- Agent 별 모델을 상이하게 적용
		- https://docs.crewai.com/core-concepts/Agents/#what-is-an-agent
	- Task 관련 문서
		- callback 사용하여 부가적인 행동 부여
		- https://docs.crewai.com/core-concepts/Tasks/
	- Crew 구성 관련 내용
		- https://docs.crewai.com/core-concepts/Crews/
	- 디렉토리 조회 툴
		- https://docs.crewai.com/tools/DirectoryReadTool/
	- 파일 조회 툴
		- https://docs.crewai.com/tools/FileReadTool/
- CrewAI와 비슷한 microsoft의 AutoGen
	- https://microsoft.github.io/autogen/
- Dashboard
	- https://docs.agentops.ai/v1/introduction




