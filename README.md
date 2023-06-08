# opensw23-team_JW

## Team Introduction

- name: 박재욱

- ID: 201911252

## Topic Introduction

> Topic: Super-SloMo

Super-SloMo는 비디오의 fps와 frame 값을 설정하여 슬로우 모션이 적용된 새로운 비디오를 얻어내는 것을 목표로 합니다. 

`fps`는 영상이 초당 몇 개의 프레임으로 구성되어 있는지를 나타내는 값으로 일반적으로 높은 FPS는 더 많은 프레임을 초당 표시하여 더 부드러운 움직임을 제공합니다. 

`Frame`수 는 영상에 포함된 실제 프레임의 수를 나타내는 것으로 `frame` 수를 증가시킴으로써 느린 속도로 재생되는 효과를 만들어낼 수 있습니다.

input으로 비디오와 옵션으로 `--fps`, `--sf`, `--output`등을 입력하면 동영상의 파일 형식, fps값, 프레임 개수 등을 이에 맞게 설정한 새로운 비디오를 얻을 수 있습니다.

이 프로젝트에서는 연속된 두 프레임을 입력으로 받아서 중간 프레임을 생성하는 영상 보간을 목표로 하며 이를 위해 멀티 프레임 보간을 위한 `end-to-end 합성곱 신경망`을 제안하고 있습니다.

# Results

> 핸드폰 카메라로 촬영한 총 8개의 영상 data set 중에서 결과값이 잘 나온 4가지 data set에 대한 결과

## Experiment 1: fps에 따른 변화 비교 (24 fps vs. 120 fps)

### 원본 영상

https://github.com/jaewook520/opensw23-team_PJW/assets/127181246/80f14a40-161b-4261-b5d3-7f8b827893ba  

### output 영상 - 1

설정 옵션:
- `Fps`: 24
- `Frame`: 3x than the original video
- `File Format`: .mp4

https://github.com/jaewook520/opensw23-team_PJW/assets/127181246/d0470a27-cf2a-4a6f-92ae-cf9ec2bd2495

### output 영상 - 2

설정 옵션:
- `Fps`: 120
- `Frame`: 3x than the original video
- `File Format`: .mp4

https://github.com/jaewook520/opensw23-team_PJW/assets/127181246/ecd48c8d-0a0f-4326-a4ef-f11e4f309ce1

## Experiment 2: Frame 수 에 따른 변화 비교 (4x vs. 6x)

### 원본 영상

https://github.com/jaewook520/opensw23-team_PJW/assets/127181246/08f1f28a-b085-4904-bcda-46a7433cdf59

### output 영상 - 1

설정 옵션:
- `Fps`: 30
- `Frame`: 4x than the original video
- `File Format`: .mp4

https://github.com/jaewook520/opensw23-team_PJW/assets/127181246/22f3dc10-be3c-4446-acd2-315ff90ae5bb

### output 영상 - 2

설정 옵션:
- `Fps`: 30
- `Frame`: 6x than the original video
- `File Format`: .mp4

https://github.com/jaewook520/opensw23-team_PJW/assets/127181246/51074c81-cc8b-48ea-8f65-9b63eacd754d

## Experiment 3: frame 수와 fps를 반비례관계로 적용

### 원본 영상

https://github.com/jaewook520/opensw23-team_PJW/assets/127181246/7e96a6c1-acaa-4102-89d0-d9f2fb83a95f

### output 영상 - 1

설정 옵션:
- `Fps`: 60
- `Frame`: 5x than the original video
- `File Format`: .mp4

https://github.com/jaewook520/opensw23-team_PJW/assets/127181246/d8cf04cc-525a-4ba4-8ac5-214ba661dd86

### output 영상 - 2

설정 옵션:
- `Fps`: 24
- `Frame`: 6x than the original video
- `File Format`: .mp4

https://github.com/jaewook520/opensw23-team_PJW/assets/127181246/c13f5a3d-59d3-4f0b-9db8-bb8d2548b84b

## Experiment 4: frame 수와 fps를 비례관계로 적용

### 원본 영상

https://github.com/jaewook520/opensw23-team_PJW/assets/127181246/a20d96cb-0060-4f57-9893-b39936f8dd25

### output 영상 1

설정 옵션:
- `Fps`: 24
- `Frame`: 6x than the original video
- `File Format`: .mp4

https://github.com/jaewook520/opensw23-team_PJW/assets/127181246/dfd1c048-540c-407f-a89b-c0146e810a02

### output 영상 2

설정 옵션:
- `Fps`: 24
- `Frame`: 2x than the original video
- `File Format`: .mp4

https://github.com/jaewook520/opensw23-team_PJW/assets/127181246/7a7ea53c-63b3-425d-a243-ae7f9ae046a9

## Analysis/Visualization

### 화질

- 영상이 보다 역동적일 수록 slow motion을 적용하였을 때, 화면이 울렁거리는 현상이 나타납니다.

- 화질이 심하게 깨지는 현상은 발생하지 않습니다.

### 재생 속도 (slow motion 적용)

- fps가 높을수록 영상이 빨라집니다.
```
FPS는 초당 표시되는 프레임의 수를 나타내기 때문에 FPS가 높을수록 초당 더 많은 프레임이 표시되어 영상이 더 빠르게 재생됩니다.
1초짜리 영상을 30FPS로 재생한다면 초당 30개의 프레임이 표시되지만 
동일한 영상을 60FPS로 재생한다면 초당 60개의 프레임이 표시되므로 영상이 0.5초 동안 재생됩니다.
```
- frame 수가 많을수록 영상이 느려집니다.
```
Frame 수가 많아지면 원본 영상의 모션을 세밀하게 나누어 표현할 수 있습니다. 
세분화된 프레임은 원래의 영상보다 매우 작은 시간 간격으로 캡처된 이미지를 나타냅니다. 
따라서 프레임 수를 늘려서 슬로우 모션을 적용하면 재생 시간을 느리게 하여 부드럽고 세밀한 영상을 보여줍니다.
```

### 기술분석

1. 가변길이의 멀티 프레임 보간:

단일 프레임 보간에 초점을 맞추는 대부분의 방법과는 다르게 해당 프로젝트에서는 가변 길이의 멀티 프레임 보간법을 사용합니다. 
이는 연속된 두 프레임 사이의 중간 프레임을 생성할 수 있다는 의미로 보다 다양한 프레임 보간 요구를 처리할 수 있고, 보간된 비디오 스퀀스의 일관성을 향상시킬 수 있습니다.

2. 공간/시간적 일관성: 

해당 프로젝트에서 제안된 방법은 시간/공간적으로 일관된 비디오 시퀀스를 형성하기 위해 설계되었습니다.
이는 중간 프레임이 공간적으로 부드럽게 이어지고, 움직임 경계 주변에서 발생하는 아티팩트를 줄이는 데 초점을 두고 있습니다. 
이를 위해 근사화된 optical flow와 가시성 맵을 사용하여 중간 프레임을 왜곡 및 융합하고, 가려진 픽셀의 기여를 배제하여 아티팩트를 방지합니다.

3. end-to-end 합성곱 신경망:

end-to-end 합성곱 신경망을 사용하여 영상 보간을 수행하는 것은 데이터의 입력부터 출력까지의 전체 과정을 하나의 네트워크로 구성하여 효율적인 학습과 예측을 가능하게 합니다.
이에 따라 전체 시스템을 최적화할 수 있고, 보간된 영상의 품질과 일관성을 향상시킬 수 있습니다.


## Installation

## 1. 실행 환경
> CPU: Intel(R) Core(TM) i5-8265U CPU @ 1.60GHz   1.80 GHz 

> Graphic Card: Intel(R) UHD Graphics 620

> OS: Window11 

> Python 3.9.11

## 2. Prerequisites (아래 파일들은 반드시 다운로드 되어야 함)
- `ffmpeg`
- `SuperSloMo.ckpt` (pretrained model trained on adobe240fps dataset)

[ffmpeg, SuperSloMo.ckpt 구글 드라이브 다운로드 링크](https://drive.google.com/drive/folders/1jmkBRSMIKqVE3b6zSCb4pn4ZT5Mn63Nu?usp=drive_link)

- 구글 드라이브를 통해 제공하는 ffmpeg: (Windows용)ffmpeg-6.0_full_build  [ffmpeg 공식 다운로드 링크](https://www.ffmpeg.org/download.html)

## 3. git clone

- 목표 디렉토리에서 아래와 같이 해당 레포지토리를 클론합니다.

```bash
git clone https://github.com/jaewook520/opensw23-team_PJW.git
```

## 4. 실행 - Convert Video

기존의 영상에 [video_to_slomo.py](video_to_slomo.py) 를 활용하여 fps를 설정하고 frame 수를 배로 증가시켜 slow-motion이 적용된 새로운 영상을 얻을 수 있습니다.

아래의 커맨드와 같이 `--sf 5`, `--fps 30` 을 argument로 주면 output 영상의 fps를 30으로 설정하고 원본 영상보다 5배 더 많은 프레임의 영상을 얻을 수 있습니다.

```주의: 아래 커맨드를 입력할 때 반드시 파일 경로를 정확히 입력해주세요```

실행 코드 예시)
```bash
# Form (Windows)
python video_to_slomo.py --ffmpeg path\to\folder\containing\ffmpeg --video path\to\video.gif --sf N --checkpoint path\to\checkpoint.ckpt --fps M --output path\to\output.mkv

# Example (Windows)
python video_to_slomo.py --ffmpeg C:\dev\openSW\opensw23-team_PJW\ffmpeg-6.0-full_build\bin --video C:\dev\openSW\opensw23-team_PJW\misc\original.gif --sf 5 --checkpoint C:\dev\openSW\opensw23-team_PJW\checkpoint\SuperSloMo.ckpt --fps 30 --output output.mkv

# About output
output 파일 형식으로 .mkv, .mp4, .gif을 제공한다.
--output output.mkv / --output output.mp4 / --output output.gif
```
특정 Library가 설치되지 않아서 위의 커맨드 실행 결과 오류가 나는 경우 다음과 같은 커맨드를 입력하여 필요한 라이브러리를 설치할 수 있습니다.
```bash
# Download Libarary which is not installed
pip install PyTorch
pip install pillow
pip install torch
pip install torchvision
pip install tqdm
```

## 5. Optional Arguments

| Optional Arguments | Description | 
|------|:-----:|
| `--h` | 옵션에 관련된 설명을 보여줌 |
| `--ffmpeg FFMPEG_DIR` | ffmpeg.exe가 존재하는 파일의 경로 | 
| `--video VIDEO` | 변환할 input 파일의 경로 |
| `--checkpoint CHECKPOINT` | 사전 훈련된 모델의 체크포인트 경로 | 
| `--fps FPS` | output 영상의 fps 값 설정. `Default: 30.` |
| `--sf SF` | SF=N일 때, N배 더 많은 프레임의 output 영상을 얻을 수 있습니다. `Example sf=2 ==> 2x frames` |
| `--batch_size BATCH_SIZE` | 더 빠른 변환을 위한 batch 크기를 지정. CPU/GPU 메모리에 따라 다름. `Default: 1` |
| `--output OUTPUT` | output 파일의 이름. 파일 형식으로는 `.mkv`, `.mp4`, `.gif`를 줄 수 있음. `Default: output.mkv` |


## Presentation
https://youtu.be/k3RXvv9VKC8
