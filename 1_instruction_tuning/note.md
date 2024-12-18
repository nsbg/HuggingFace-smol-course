# [정리] Instruction tuning
## Chat Templates
- LLM을 채팅으로 사용하는 사례 증가
    - 모델은 하나 이상의 `메시지`로 구성된 대화를 이어나갈 수 있음
    - 각 `메시지`에는 user, assistant 같은 역할과 메시지 내용인 텍스트가 포함됨

- 대화 형식은 모델에 따라 다양함
    - [mistralai/Mistral-7B-Instruct-v0.1 vs HuggingFaceH4/zephyr-7b-beta](./chat_templates.ipynb)
    - 위의 두 모델은 모두 `Mistral-7B-v0.1`을 파인튜닝한 모델이지만 대화 형식이 다름

- tokenizer.apply_chat_template(conversation, tokenize: bool, add_generation_prompt: bool)
    - **conversation**: "role"과 "content" 키로 이루어진 딕셔너리가 들어 있는 리스트로, 지금까지의 채팅 기록을 의미함
    - **tokenize**: 결과 토큰화 여부 설정(True가 디폴트) -> False면 결과는 문자열로 출력됨
    - **add_generation_prompt**: chat template에 모델(허깅페이스는 봇으로 표현) 응답 시작을 알리는 토큰을 추가

- Default ChatML(Chat Markup Language)
    ```
    <|im_start|>system 
    Provide some context and/or instructions to the model.
    <|im_end|> 
    <|im_start|>user 
    The user’s message goes here
    <|im_end|> 
    <|im_start|>assistant
    ```
## Supervised Fine-Tuning