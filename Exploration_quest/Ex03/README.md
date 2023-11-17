# README

- 작성자 : 이혁희
- 코드 : "6. 인물사진을 만들어보자.[프로젝트].ipynb"

## 이미지 segmentation과 아웃포커싱/합성
PASCAL Voc 이미지로 학습된 모델을 이용해서 이미지를 segmentation하고(PixelLib 패키지 사용) segmentation된 부분을 이미지 마스크로 사용하여 아웃포커싱과 크로마키 합성하는 실습을 해 보았습니다.

이미지 합성은 다음과 같은 과정을 거쳐서 진행하였습니다.
- 이미지 segmentation 하기
- 특정 segment(예: person)에 대한 이미지 마스크 만들기
- 합성할 배경이미지 처리(blur 처리 or 이미지 사이즈 맞추기)
- 두개의 이미지를 이미지 마스크에 맞춰서 합성(mask된 부분: 인물/고양이, 안된 부분 : 배경)
- 합성된 이미지 저장


## 합성이미지의 문제점과 해결책
합성된 이미지는 합성된 경계면이 고르지 못한 문제점이 있었습니다. 특히, 머리카락이나 고양이 수염처럼 가늘고 긴 물체가 있을 때 해당 물체을 잘라 먹거나 원본의 배경이 그대로 표시되는 문제가 있었습니다. 또, 털 스웨터 등은 합성면이 거칠게 표현되었습니다.

문제 해결을 위하여 모폴로지 연산, 가우시안 블러 기법을 적용하였습니다. 이를 통해 합성 표면이 정리되는 효과는 있었지만, 위에서 이야기한 문제를 해결하지는 못하였습니다.


## 함수 정리
반복적으로 나오는 코드는 prep.py에 정리하였습니다.

- build_model : pixellib.semantic_segment를 이용하여 모델을 생성하고 다운받은 모델을 로드한다.
- get_seg_color : 주어린 라벨에 해당하는 영역의 색상표(BRG)를 리턴한다.


## 회고

### 잘한 점
- semantice segmentation을 잘 모르지만 라이브러리를 사용하여 segmenation을 이용한 이미지 아웃포커싱과 합성을 해냈다.

### 문제점
- 고양이 수염이 잘리는 문제와 머리카락 안쪽 배경이 나타나는 문제의 완전한 해결책을 못찾았다.

### 배운 점
- 바닥부터 만들 생각을 하면 시작도 못한다. 남이 잘 만들어 놓은 것을 열심히 갖다 쓰자!