# 캐릭터 자판기

- [소스](https://drive.google.com/open?id=1nhzfn6gmrHa6hmn5JKyG0JgBYWUxpnix)
- 데이터 [64 x 64 게임 캐릭터 이미지](https://drive.google.com/file/d/1Z-6c61dPqspxCrs7vQ4ZIDIdqGa47i9-/view)
[128 x 128 게임 캐릭터 이미지](https://drive.google.com/open?id=1a_YG1Ny8qQZOgaVlpkNwu6bg1-MNlxi3)

## 개발환경 및 데모 스펙
- AI 개발환경
   - Docker 환경구성
      - Ubuntu 16.04, CUDA 8.0, cuDNN 8.0.61
   - 프레임워크(버전)
      - Tensorflow 1.4
   - 언어(버전)
      - Python3
   - 기타(IDE 등)
      - spyder3, openCV3, theano, pyqt4, hdf5
- 데모 스펙
   - HW(장비포함)
      - 운영체제 : Linux ktai03-Alienware-Aurora-R7 4.13.0-43-generic #48~16.04.1-Ubuntu SMP Thu May 17 12:56:46 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux
      - 프로세서 :  Intel(R) Core(TM) i7-8700K CPU @ 3.70GHz
      - 메모리 : 31GiB
   - SW
      - GUI: pyqt4

### SR-GAN 실행 후 새로운 terminal에서 iGAN 실행

1. SR-GAN
1.1 [R-GAN 도커 이미지](https://hub.docker.com/r/oyj9097/srgan/) 다운로드
   ```
   $ docker pull oyj9097/srgan:2
   ```
1.2 도커 설정 
   ```
   $ nvidia-docker run -it --net=host -e DISPLAY -v /tmp/.X11-unix -p 8888:8888 -v /home/ktai02/Documents/workspace:/workspace --name srGAN {도커이미지아이디} /bin/bash 9bb283c95227
   ``` 
1.3 실행
   ```
   $ python main.py --mode=evaluate
   ```


2. iGAN
2.1 [iGAN 도커 이미지](https://hub.docker.com/r/ggmmjj1/mini4/) 다운로드
   ```
   $ docker pull ggmmjj1/mini4
   ```
2.2 도커 설정 
   ```
   $ nvidia-docker run -it --net=host -e DISPLAY -v /tmp/.X11-unix -p 8888:8888 -v /home/ktai02/Documents/workspace:/workspace --name iGAN {도커이미지아이디} /bin/bash
   ```
2.3 xauth host 설정 (xauth list, xauth add ~)
2.4 모듈 추가
   ```
   $ pip install --upgrade --no-deps git+git://github.com/Lasagne/Lasagne.git
   ```
2.5 환경변수 설정
   ```
   $ export QT_X11_NO_MITSHM=1
   ```
2.6 실행 
   ```
   $ THEANO_FLAGS='device=gpu0, floatX=float32, nvcc.fastmath=True' python iGAN_main.py --model_name charac_64 --win_size 600
   ```
2.7 저장
2.7.1 기능 1(파일 첨부) 실행 후 고해상도 캐릭터 이미지로 변환하여 지정폴더('iGAN-master/super_pics/')에 자동 저장
2.7.2 기능 2(그림 그리기) 실행 후 save버튼 누르면 고해상도 캐릭터 이미지로 변환하여 선택한 폴더에 자동 저장
