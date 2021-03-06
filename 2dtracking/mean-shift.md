# Mean Shift 상세 

    Hill Climb 탐색 방법
    . Mean Shift
    . gradient descent search
    . blind search
    . greedy search

## 1. 정의 

사용자가 설정한 ROI 데이터(특징점,코너,색상) 밀도 분포의 peak 또는 무게중심을 찾아 간다.

![](https://i.imgur.com/vesFsJJ.png)

단계
1. 현재 위치에서 반경 r 이내에 들어오는 데이터들을 구한다: (x1,y1), (x2,y2), ..., (xn,yn)
2. 이들의 무게중심의 좌표 (∑xi/n, ∑yi/n)로 현재 위치를 이동시킨다.
3. 1~2 과정을 위치변화가 거의 없을 때까지, 즉 수렴할 때까지 반복한다.


기본 아이디어 (eg. 색상 히스토그램 이용시  :ROI중심으로 일정 거리 내에서(탐색 윈도우) 가장 비슷한 히스토그램을 쫒아다니는 방식으로 물체를 추적한다.)

![](https://i.imgur.com/mE4DzLD.png)
추적하고자 하는 대상 물체에 대한 색상 히스토그램(histogram)과 현재 입력 영상의 히스토그램을 비교해서 가장 유사한 히스토그램을 갖는 윈도우 영역을 찾는 것이다. 
- 단점 : 모든 가능한 윈도우 위치에 대해 각각 히스토그램을 구하고 또 비교해야 하기 때문에 시간이 너무 오래 걸린다.

개선 방안 

![](https://i.imgur.com/F3HdjLB.png)
histogram backprojection 기법과 mean shift를 결합한 방법
- 먼저, 영상에서 추적할 대상 영역이 정해지면 해당 윈도우 영역에 대해 히스토그램을 구하여 객체 모델로 저장한다. 
- 이후 입력 영상이 들어오면 histogram backprojection을 이용해서 입력 영상의 픽셀값들을 확률값으로 변경시킨다. 
- 이렇게 구한 확률값 분포에 대해 mean shift를 적용하여 물체의 위치를 찾는다. 
- 만일 물체의 크기 변화까지 따라가고 싶은 경우에는 찾아진 위치에서 윈도우의 크기를 조절해 가면서 저장된 모델과 가장 히스토그램 유사도가 큰 스케일(scale)을 선택한다.


## 3. 절차 

[[영상추적#1] Mean Shift 추적](http://darkpgmr.tistory.com/64?category=460965)..참고 



## 4. 문제점
- 탐색윈도우가 작을 때는 Local minimum 에 빠져서 더 이상 추적이 불가능하다.
- 영상속의 물체가 커지거나 작아져도 ROI 크기가 일정하다.
- 색상히스토그램을 사용하는 경우 조도변화나 잡음이 많은 환경에서는 성능이 좋지 않다.


![](http://img1.daumcdn.net/thumb/R1920x0/?fname=http%3A%2F%2Fcfile22.uf.tistory.com%2Fimage%2F1606F43C4EF8F8532B803B)
위 그림처럼 Local Minimum에 빠진다. 



---


### CAM(Continuously Adaptive Mean) shift 상세 

특징 : Mean shift의 문제점 중 ROI크기가 일정하다는 문제점을 해결하여 ROI크기가 매번 바뀔 수 있고,회전변화에도 추적이 가능하다.
- 탐색윈도우의 크기를 스스로 조정하는 기법을 사용하여 Mean-shift의 답점을 보강한다.


검출된 객체의 영역의 Hue 값의 분포를 이용하여 변화될 위치를 예측하고 탐지한 후 중심을 찾아 객체를 추적하게 된다. 
- 상대적으로 Hue 값을 사용하면 조명의 영향에 덜 민감하므로 Hue값을 사용한다


단점 : 조도변화, 잡음이 많은 배경에서는 성능이 좋지않은 특징

![](https://i.imgur.com/CZeuyTR.png)

단계
1. 관심영역(ROI)이 주어지면 HSV 색 모델의 Hue값으로 변환한다. 
2. ROI에서 1차원 histogram을 구축하여 저장하고 추적 모델로 사용한다.
3. ?

---

[비디오 처리 - MeanShift, CamShift](https://blog.naver.com/warchife/221136545517)

[[영상추적#1] Mean Shift 추적](http://darkpgmr.tistory.com/64?category=460965)

[OpenCV의 MeanShift / CamShift 추적기](http://darkpgmr.tistory.com/111): C++코드 

[비디오에서 객체 추적하기1 -  Meanshift 살펴보기](http://sams.epaiai.com/220658244422) : python

[비디오에서 객체 추적하기2 - CamShift](http://sams.epaiai.com/220659310860): python

