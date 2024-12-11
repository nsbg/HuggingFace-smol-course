# [정리] Instruction tuning
## Chat Templates
- LLM을 채팅으로 사용하는 사례 증가
    - 모델은 하나 이상의 `메시지`로 구성된 대화를 이어나갈 수 있음
    - 각 `메시지`에는 user, assistant 같은 역할과 메시지 내용인 텍스트가 포함됨
- 대화 형식은 모델에 따라 다양함
    - [mistralai/Mistral-7B-Instruct-v0.1 vs HuggingFaceH4/zephyr-7b-beta](./chat_templates.ipynb)
    - 위의 두 모델은 모두 `Mistral-7B-v0.1`을 파인튜닝한 모델이지만 대화 형식이 다름
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