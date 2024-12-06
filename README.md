# Installation
Although the installation instructions are available on Hugging Face's official GitHub, this repository provides a more detailed guide on setting up the environment using the `uv` package on the Windows operating system.

**⚠️ If you notice any typos or issues, feel free to let me know anytime!**

## 1. Install uv on Windows powershell
```
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

## 2. Set environment variable PATH
If the uv package has been installed successfully, you will see the following message:
```
To add C:\Users\username\.local\bin to your PATH, either restart your system or run:

    set Path=C:\YOUR\DIRECTORY\.local\bin;%Path%   (cmd)
    $env:Path = "C:\YOUR\DIRECTORY\.local\bin;$env:Path"   (powershell)
```

Copy and enter the command corresponding to the terminal you are using.

```Powershell
C:\YOUR\WORKING\DIRECTORY> $env:Path = "C:\YOUR\DIRECTORY\.local\bin;$env:Path"
```

## 3. Download Python
```
uv python install 3.11
```
You can download multiple Python version at once:
```
uv python install 3.10 3.11 3.12
```

## 4. Create and work on Python project
```
uv venv --python 3.11.10

uv init YOUR_PROJECT_DIRECTORY

uv sync
```
`uv sync` means 'Sync the project's dependencies with the environment.'

# Tips
If you have finished setting up the environment variables but see the following message when running the uv command, close the current window (e.g., VSCode, terminal, etc.) and try running the command again.
## Kor
```
uv : 'uv' 용어가 cmdlet, 함수, 스크립트 파일 또는 실행할 수 있는 프로그램 이름으로 인식되지 않습니다. 이름이 정확한지 확인하고 경로가 포함된 경우 경로가 올바른지 검증한 다음 다시 시도하십시오.
```
## Eng
```
uv: The term 'uv' is not recognized as the name of a cmdlet, function, script file, or operable program. ...
```

# References
- https://docs.astral.sh/uv/
- https://github.com/astral-sh/uv
- https://github.com/huggingface/smol-course

