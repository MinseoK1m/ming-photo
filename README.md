# ming-photo
* openCV 라이브러리를 활용한 포토샵 프로그램
* 2023-2학기 [영상처리 프로그래밍] 기말 프로젝트
* 2023.11.19-2023.12.10
* Python, jupyter notebook, QT Designer

* 수행 계획
  ![그림1](https://github.com/MinseoK1m/ming-photo/assets/138808284/1b9112c1-3964-4dd6-a585-e9b2e56fe2f0)

* 기능구현 세부계획
  ![image](https://github.com/MinseoK1m/ming-photo/assets/138808284/c59e01f5-290f-4c09-9129-6edf6ab6a04f)

* 메뉴구성도
  ![image](https://github.com/MinseoK1m/ming-photo/assets/138808284/da15c149-6e6c-43bd-9d00-e515cd8b16da)


* GUI 디자인
  * QT Designer를 사용하여 UI디자인 후 python코드로 변환 후 적용
     ![image](https://github.com/MinseoK1m/ming-photo/assets/138808284/ced53a50-0243-4636-9760-7ebdd494535b)
      ![image](https://github.com/MinseoK1m/ming-photo/assets/138808284/b15bbe67-5978-41a8-8d0e-a023d5a01a13)
    ![image](https://github.com/MinseoK1m/ming-photo/assets/138808284/91dc1872-efe9-4196-9212-1a36b6baf595)


* 구현 기능
  * 카메라
    * 사진 촬영, 확대/축소 기능
      - 카메라 출력 -> cv2.VideoCapture(0)
      
      - 확대 -> 슬라이더 value값, cv2.resize(frame, 값)
      
      - 좌우반전 -> cv2.flip(frame, 1)
       ![image](https://github.com/MinseoK1m/ming-photo/assets/138808284/26a178bc-992d-471b-8f97-484ffeaa2f7b)


  * 이미지 편집 기능
    * 사용자가 파일에서 사진을 가져와 사진 꾸미기를 진행할 수 있도록 함.
    * 사진 고르기

      : QFileDialog.getOpenFileName()을 사용하여 파일 속에서 사진을 고르면, 그 파일의  경로를 저장하여 이미지를 끌어옴
    - 밝기/대비 조절 기능
      : -99~99까지의 값을 사용자에게 슬라이더로 받아, 정도에 따른 밝기와 대비를 이미지에 적용함
      : cv2.convertScaleAbs()에 알파, 베타 값을 넣어 구현함
      
      ![image](https://github.com/MinseoK1m/ming-photo/assets/138808284/927449b5-af86-4099-bec4-5b5d4d3f120f)
      
    - 자르기 기능
      : selectROI()를 사용하여 좌표 4개를 받아, 그 좌표에 맞는 이미지만 출력하여 자르기 기능을 구현함
      
      ![image](https://github.com/MinseoK1m/ming-photo/assets/138808284/437bc5de-1eb6-46b7-8319-52ec46cbf146)
      
    - 좌우 반전 기능
      : cv2.flip(img, 1)을 사용해 간단하게 좌우반전을 구현함
      
      ![image](https://github.com/MinseoK1m/ming-photo/assets/138808284/6001ec7b-3ad3-4d5d-9c6e-391188ff963b)
      
    - 오른쪽 90도 회전 기능
      : cv2.rotate(img,cv2.ROTATE_90_CLOCKWISE)를 사용하여, 시계방향(오른쪽)으로 이미지가 90도씩 회전하는 기능을 구현
      
      ![image](https://github.com/MinseoK1m/ming-photo/assets/138808284/0febf9eb-d6be-4bfc-93fb-fe8d4ce4e7ca)
 
    - 색상표
      : openCV에는 색상표 기능이 없어 QT라이브러리의 QColorDialog.getColor()를 사용
      
    - 그리기 도구 두께 설정
      : 사용자가 GUI의 spinBox에서 value값을 입력하면, 변수에 저장해두고 그림을 그릴 때 적용하도록 하였음
 
    -  펜 기능 (그림 그리기)
      : 마우스 이벤트가 발생할 때, 좌표를 받아 cv2.line함수를 pt1과 pt2가 같을 때 호출하여     그림을 그리는 함수를 구현하였음.
      : 반짝거리는 선을 구현하기 위해, 선그리기 함수와 원그리기 함수를 동시에 호출하여 선 뒤   로 하얀 동그라미들이 생기게 하여 반짝이는 효과를 구현하였음.

       ![image](https://github.com/MinseoK1m/ming-photo/assets/138808284/e8921ea8-9492-468f-8c25-986788f2bbb9)

    - 필터 기능
      * 흑백 : cv2.cvtColor()함수와 cv2.COLOR_RGB2GRAY코드 값을 이용하여 구현함
      * 부드럽게 : cv2.blur()함수로 구현함
      * 선명하게 : sharpening필터를 생성하고, cv2.filter2D를 이용해 필터를 적용하여 구현함
    
       ![image](https://github.com/MinseoK1m/ming-photo/assets/138808284/176941c6-e9b3-4db4-ac97-6f99747d5f10)

     - 모자이크 기능
      : selectROI를 호출하여 원하는 범위를 입력받아, 그 범위에 cv2.blur()를 적용하여 구현함
  
       ![image](https://github.com/MinseoK1m/ming-photo/assets/138808284/5c565304-e3dd-4e85-ab1e-35a2e4673fd5)
  
     -  스티커 붙이기 기능, snow 효과 기능
        1. 이미지에서 스티커를 붙일 영역을 지정해 변수 roi에 저장
        2. 스티커의 알파 채널을 가져와 크기를 조절하고 마스크를 생성
        3. roi와 같은 크기의 검은색 초기 마스크를 만들고, 알파 채널 값을 이용해 마스크를 업데이트 함
        4. 마스크를 활용해 스티커와 roi를 결합하여 최종 이미지를 만듦
         
         ![image](https://github.com/MinseoK1m/ming-photo/assets/138808284/c0c617bf-0a15-40c3-a86e-909effbb897d)
  
    - 앨범 만들기 기능
        1. 이미지들을 사용자가 4개를 불러와 변수에 저장
        2. 이미지들의 중심을 기준으로 비율에 맞게 자르고, 4개의 이미지를 2x2로 배열
        3. 프레임의 크기에 맞도록 2x2 이미지 크기를 조절함
        4. 위의 스티커 붙이기 기능 함수를 재사용하여 프레임을 씌워줌
  
       ![image](https://github.com/MinseoK1m/ming-photo/assets/138808284/b8fbe376-b9d5-4802-ae94-22001f07c945)


# 마무리하며

  이 프로젝트는 [영상처리프로그래밍] 기말 프로젝트로 제작한 것이다.
  
  개발 기간은 약 1달이 주어졌으며, 교수님이 어느정도 틀을 제시해주셨다.

  내가 만든 프로그램이 그저 과제로 제출한 느낌이 아닌 '누군가가 사용할 것이라는 전제'로 만들어진 완성도 높은 프로그램, 또 사용자가 불편한 점이 없었으면 좋겠다고 생각했다.
  그래서 GUI디자인에서 시간을 많이 쓰기도 했고, 사이에 변경사항도 많았었다.
  또한 교수님이 제시한 기능들 외에 부가적인 요소들을 완성도를 높이기 위해 구현해야했다.
  
  중간점검에서 교수님이 내가 디자인한 UI를 보고 걱정하시기도 했고, 일단은 기능을 구현하는 것에 집중을 해야할 것 같다는 충고도 해주셨다.
  
  기능 구현에 힘든 점들도 많았고, 후반부에 몸이 좋지않아서 체력적으로 힘들었지만,
  잘 해낸 것 같아서 뿌듯한 프로젝트다.

  내가 직접만든 프로그램으로 내 사진을 꾸미고 수정할 수 있다는 게, 개발의 재미를 한 번 더 와닿게 해줬던 것 같다.
