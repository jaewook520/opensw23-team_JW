# opensw23-team_JW

## Team Introduction

- name: 박재욱

- ID: 201911252

## Topic Introduction

- Topic: Super-SloMo
- 출처: https://github.com/avinashpaliwal/Super-SloMo

## Results

### original video
![original](https://github.com/jaewook520/opensw23-team_PJW/assets/127181246/da4ec5f2-13ba-496d-b031-ac1e61ed6fb2)

### output video
#### Changes

- converted to 30fps
- 2x frames than the original video

![output](https://github.com/jaewook520/opensw23-team_PJW/assets/127181246/a3730f3e-9c53-4125-952e-75502c033f0d)

output video의 파일 확장자는 본래 .mkv 이다.

위의 output 동영상은 편의를 위해 .mkv를 .gif로 파일 변환한 것임을 밝힘.

동영상 파일 변환 링크: https://cloudconvert.com/mkv-to-gif

## Installation

#### Prerequisites
- ffmpeg
- SuperSloMo.ckpt (pretrained model trained on adobe240fps dataset)
- PyTorch

[CLICK HERE to download ffmpeg, SuperSloMo.ckpt](https://drive.google.com/drive/folders/1jmkBRSMIKqVE3b6zSCb4pn4ZT5Mn63Nu?usp=drive_link)

위의 구글 드라이브를 통해 제공하는 ffmpeg의 버전은 (Windows용)ffmpeg-6.0_full_build이다. [ffmpeg 공식 다운로드 링크](https://www.ffmpeg.org/download.html)

PyTorch 설치
```
pip install PyTorch
```

git clone
```
git clone https://github.com/jaewook520/opensw23-team_PJW.git
```

Convert Video

[video_to_slomo.py](video_to_slomo.py) 를 활용하여 동영상에 slow-motion을 적용하거나 fps를 바꿀 수 있다.

아래와 같이 `--sf 2`, `--fps 30` 을 argument로 주면 output 영상의 fps를 30으로 설정하고 원본 영상보다 3x 프레임 더 한 영상을 얻을 수 있다.

```bash
# Form (Windows)
python video_to_slomo.py --ffmpeg path\to\folder\containing\ffmpeg --video path\to\video.mp4 --sf N --checkpoint path\to\checkpoint.ckpt --fps M --output path\to\output.mkv

# Example (Windows)
python video_to_slomo.py --ffmpeg C:\dev\openSW\opensw23-team_PJW\ffmpeg-6.0-full_build\bin --video C:\dev\openSW\opensw23-team_PJW\misc\original.gif --sf 2 --checkpoint C:\dev\openSW\opensw23-team_PJW\checkpoint\SuperSloMo.ckpt --fps 30 --output output.mp4
```

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
