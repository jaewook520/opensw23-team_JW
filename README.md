# opensw23-team_JW

## Team Introduction

- name: 박재욱

- ID: 201911252

## Topic Introduction

- Topic: Super-SloMo

Super-SloMo는 비디오의 fps와 frame 값을 설정하여 슬로우 모션이 적용된 새로운 비디오를 얻어내는 것을 목표로 합니다. frame은 초당 표시되는 정지 이미지의 수를 나타내는 것으로 frame 수를 증가시킴으로써 느린 속도로 재생되는 효과를 만들어낼 수 있습니다.

연속된 두 프레임이 주어졌을 떄, 영상 보간은 공간/시간적으로 일관된 비디오 스퀀스를 형성하기 위해 중간 프레임을 생성하는 것을 목표로 합니다. 대부분의 기존 방법은 단일 프레임 보간에 초점을 맞추지만, 해당 프로젝트에서는 가변 길이의 멀티 프레임 보간을 위한 end-to-end 합성곱 신경망을 제안합니다.

먼저, U-Net 아키텍처를 사용하여 입력 이미지 간의 양방향 optical flow를 계산합니다. 이러한 플로우는 각 시간 단계에서 선형적으로 결합되어 중간 양방향 optical flow를 근사화합니다. 

하지만 이 근사 flow는 지역적으로 매끄러운 영역에서만 잘 작동하고, 움직임 경계 주변에 아티팩트를 생성합니다. 이러한 단점을 해결하기 위해, 다른 U-Net을 사용하여 근사화된 flow를 개선하고 부드러운 가시성 맵을 예측합니다. 

마지막으로, 두 입력 이미지는 왜곡되고 선형적으로 융합되어 각 중간 프레임을 형성합니다. 융합 전에 왜곡된 이미지에 가시성 맵을 적용하여 가려진 픽셀의 기여를 배제하여 아티팩트를 방지합니다. 학습된 네트워크 매개변수는 시간에 따라 변하지 않으므로, 이러한 접근 방식은 필요한 만큼 많은 중간 프레임을 생성할 수 있습니다. 

해당 프로젝트에서는 240프레임씩 1,132개의 비디오 클립을 사용하여 네트워크를 학습시킵니다. 다양한 개수의 보간된 프레임을 예측하는 여러 data set의 실험 결과는, 이러한 접근 방식이 기존 방법보다 일관되게 더 나은 성능을 발휘함을 보여줍니다.

####

## Results

### original video
![original](https://github.com/jaewook520/opensw23-team_PJW/assets/127181246/da4ec5f2-13ba-496d-b031-ac1e61ed6fb2)

### output video
![output (2)](https://github.com/jaewook520/opensw23-team_PJW/assets/127181246/09d52233-17c0-4f48-8c9b-1f41f9b15d0d)


#### Changes

- converted to 30fps
- 5x frames than the original video (slow-motion)


output video의 파일 확장자는 본래 .mkv 이지만 위의 output 비디오는 편의를 위하여 .mkv를 .gif로 파일 변환한 파일을 업로드 하였습니다.

- 동영상 파일 변환 링크(mkv-to-gif): https://cloudconvert.com/mkv-to-gif

## Installation

#### Prerequisites (아래 파일들은 반드시 다운로드 되어야 함)
- ffmpeg
- SuperSloMo.ckpt (pretrained model trained on adobe240fps dataset)

[CLICK HERE to download ffmpeg, SuperSloMo.ckpt](https://drive.google.com/drive/folders/1jmkBRSMIKqVE3b6zSCb4pn4ZT5Mn63Nu?usp=drive_link)

- 구글 드라이브를 통해 제공하는 ffmpeg: (Windows용)ffmpeg-6.0_full_build  [ffmpeg 공식 다운로드 링크](https://www.ffmpeg.org/download.html)

#### git clone

```bash
git clone https://github.com/jaewook520/opensw23-team_PJW.git
```

#### Convert Video

동영상은 [video_to_slomo.py](video_to_slomo.py) 를 활용하여 fps를 설정하고 frame 수를 배로 증가시켜 slow-motion이 적용된 새로운 영상을 얻을 수 있습니다.

아래의 커맨드와 같이 `--sf 5`, `--fps 30` 을 argument로 주면 output 영상의 fps를 30으로 설정하고 원본 영상보다 5배 더 많은 프레임의 영상을 얻을 수 있습니다.

```bash
# Form (Windows)
python video_to_slomo.py --ffmpeg path\to\folder\containing\ffmpeg --video path\to\video.gif --sf N --checkpoint path\to\checkpoint.ckpt --fps M --output path\to\output.mkv

# Example (Windows)
python video_to_slomo.py --ffmpeg C:\dev\openSW\opensw23-team_PJW\ffmpeg-6.0-full_build\bin --video C:\dev\openSW\opensw23-team_PJW\misc\original.gif --sf 5 --checkpoint C:\dev\openSW\opensw23-team_PJW\checkpoint\SuperSloMo.ckpt --fps 30
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
- video_to_slomo.py

| Optional Arguments | Description | 
|------|:-----:|
| --h | show this help message and exist |
| --ffmpeg FFMPEG_DIR | path to ffmpeg.exe | 
| --video VIDEO | path of video to be converted |
| --checkpoint CHECKPOINT | path of checkpoint for pretrained model | 
| --fps FPS | specify fps of output video. Default: 30. |
| --sf SF | specify the slomo factor N. This will increase the frames by Nx. Example sf=2 ==> 2x frames |
| --batch_size BATCH_SIZE | Specify batch size for faster conversion. This will depend on your cpu/gpu memory. Default: 1 |
| --output OUTPUT | Specify output file name. Default: output.mp4 |


## Presentation
