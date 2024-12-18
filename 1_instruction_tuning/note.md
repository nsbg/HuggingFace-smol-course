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
- 모델 학습에서 **step**
    - 하나의 배치가 모델에 입력되어 순전파, 역전파, 가중치 업데이트가 이루어지는 과정이 1 step
    - Step 수는 학습 속도 및 총 학습 시간에 직접적인 영향을 미침

- Step과 Epoch의 관계
    - **Epoch**는 전체 데이터셋을 한 번 학습하는 과정
    - 데이터셋 크기가 `N`이고 배치 크기가 `B`이면 한 epoch는 `N/B step`
        
        #### 예)
        - 전체 데이터셋: 10,000개
        - 배치 사이즈: 100
        - 1 epoch: 10000/100 = 100 step
- SFTConfig
    - **max_steps**

        - 지정한 max_steps 값만큼 학습 진행
        - max_steps가 지정돼있을 경우 num_train_epoch를 무시함
        - 데이터셋에 포함된 모든 샘플이 사용된 후에도 max_steps에 도달하지 못했다면 데이터셋을 반복적으로 사용
        - Default -1

    - **per_device_train_batch_size**
    
        - 학습 시 각 GPU/TPU/CPU에서 처리할 배치 사이즈 지정
        - Default 8

    - **evaluation_strategy**

        - "no": 학습 중 평가 과정 없음
        - "steps": `eval_steps` 기준으로 평가 진행 후 로그 기록
        - "epoch": `epoch`가 한 번 끝날 때마다 평가 진행

    - **eval_steps**
        - `evaluation_strategy="steps"`일 때 지정한 step 간격만큼 평가 진행 