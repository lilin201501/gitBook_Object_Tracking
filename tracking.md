# Tracking 개요


Tracking 정의 : locating an object in successive frames of a video


### Object Tracking관련 아이디어들

- Dense Optical flow: These algorithms help estimate the motion vector of every pixel in a video frame.

- Sparse optical flow: These algorithms, like the Kanade-Lucas-Tomashi (KLT) feature tracker, track the location of a few feature points in an image.

- Kalman Filtering: A very popular signal processing algorithm used to predict the location of a moving object based on prior motion information. One of the early applications of this algorithm was missile guidance! Also as mentioned here, “the on-board computer that guided the descent of the Apollo 11 lunar module to the moon had a Kalman filter”.

- Meanshift and Camshift: These are algorithms for locating the maxima of a density function. They are also used for tracking.

- Single object trackers: In this class of trackers, the first frame is marked using a rectangle to indicate the location of the object we want to track. The object is then tracked in subsequent frames using the tracking algorithm. In most real life applications, these trackers are used in conjunction with an object detector.

- Multiple object track finding algorithms: In cases when we have a fast object detector, it makes sense to detect multiple objects in each frame and then run a track finding algorithm that identifies which rectangle in one frame corresponds to a rectangle in the next frame.

### Tracking vs Detection


> 추가 내용 살펴 보기 : https://www.learnopencv.com/object-tracking-using-opencv-cpp-python/

---
# 이미지 기반 트래킹

추적 알고리즘 분류 \#1

* 결정론적 방법 : Local Search
* Least-Square tracking
* Mean-Shift
* Gradient ascent/decent 알고리즘
* 확률론적 방법 : Probabilistic search
* Kalman Filter
* extended kalman Filter
* Particle Filter

Basic Tracking Algorithm

* centroid tracking : it relies on the Euclidean distance between
* \(1\) existing object centroids \(i.e., objects the centroid tracker has already seen before\) and
* \(2\) new object centroids between subsequent frames in a video.

Advanced Tracking Algorithm

* kernel-based
* correlation-based

추적 알고리즘 분류 \#2

* Mean Shift,
* CAMshift,
* ABCshift,
* 칼만 필터,
* 비선형 칼만 필터,
* 입자 필터

그 중 Mean Shift, CAMshift ABCshift 알고리즘은 탐색 윈도우 를 통하여 추적물체의 영역 및 중심을 계산한다.

Mean Shift\(평균이동알고리즘\)는

* 데이터 집합의 밀도분포를 기반으로 관심영역 객체를 고속으로 추적하는 알고리즘으로서 초기의 검색 영역의 크기와 위치를 지정하면 반복적인 색 분할 계산으로 색상 클러스터가 발생하고 초기 지정한 색 영역에 기반을 두어경계를 결정하여 관심 물체를 추출하게 된다\[4\].
* Tracks objects by finding the maximum density of a discrete sample of a probability function

Mean Shift 알고리즘을 개량한 CAMshift 알고리즘은 1998년 GR Gradski에 의해 처음 소개되었다\[5\].

* Color Segment 방법의 Mean Shift 알고리즘을 연속적인 입력 영상에서 사용하기 위해 개선한 것으로 탐색 윈도우의 크기를 스스로 조정하는 기법을 사용하여 능동적으로 변화하는 객체의 크기를 검출하고 추적해낼 수 있다.

ABCshift 알고리즘은

* CAMshift 방법과 유사하나 복잡한 색상의 배경에 적응하여 객체를 배경과 따로 분리하는 효과를 얻어서 객체와 같은 색상이 등장하는 상황 중에도 강인한 추적을 보인다\[7\]. 　

칼만 필터, 확장 칼만 필터, 입자 필터는 오차가 포함된 현재 시스템 측정값이나 관측값을 바탕으로 미래정보를 예측하는 알고리즘이다.

칼만 필터는 루프만 칼만에 의해 1960년대 초 개발된 필터로 순환적선형구조로 되어 있고 단순하며 수렴 성이 좋다.

칼만 필터는 수식을 이용하여 직접적인 예측이 가능하므로 컴퓨터 시스템을 이용하여 추적할 때 적합한 방법이다\[8\].

그리고 입자 필터\(Particle Filter\)를 이용한 추적은 시스템에 가우시안 확률분포로 임의로 생성된 입력을 종합하여 추적이 이루어지도록 하는 방법이다.

* Particle Filter 알고리즘은 객체가 가려지는 상황에 강인하므로, 이 특성을 이용한 부분색상정보 기반의 추적 시스템이 개발되었다\[9\].
* 일반적으로 물체의 선형적인 운동에는 칼만 필터가 사용되고 비선형적 운동에는 확장 칼만 필터나 입자 필터가 사용된다.

Manya Afonso는 대표적인 비선형 예측 알고리즘인 확장 칼만 필터와 입자 필터에 대해 비교 분석하였다\[10\].

혼합방식 : 위에 소개된 알고리즘들이 갖고 있는 장점을 취하고 단점을 보완하기 위해 각각의 알고리즘을 통합하여 객체를 추적하려는 시도도 이루어지고 있다.

그예로 칼만 필터와 CAMshift 알고리즘을 결합하여 추적객체의 가려짐에 강건한 추적에 관한 연구가 진행되었다\[11,12\].

* 탐색 윈도우 예측 시 물체의 속도만을 반영하고 CAMshift에 의해 구한 중심벡터 이동정보를 활용하지는 않았다.

색상객체의 추적을 위한 또 다른 추적모듈 결합방법으로 칼만 필터와 입자 필터의 결합에 대해 다룬논문도 소개되었다\[13\].

* 선형 필터인 칼만 필터는 선형 운동을 하는 객체의 추적을, 비선형 운동을 하는 객체의 추적은 입자 필터를 이용하여 추적한 점이특징이다.

또한, 추적되는 색상객체를 SURF 알고리즘을 이용하여 인식하고 칼만 필터를 결합하여 움직임을 예측한 방법도 연구된 바가 있다\[14\].

> CAMshift 기법과 칼만 필터를 결합한 객체 추적 시스템, 김대영, 2013

---

**이동물체 추적기법**은 그 처리방법에 따라 분류할 경우 **정합기반기법**과 **에너지기법**으로 분류할 수 있다.

정합기반기법

* 추적대상의 윤곽선, 모서리, 휘도 혹은 색상분포를 가지고 추적대상의 모델ㅇ르 구성하여 화면 내에서 이와 유사한 부분을 탐색하는 방법으로 탐색과 정합 두 가지 단계로 구성된다.
* 정합기반 방법은 탐색과정을 거쳐 이동물체의 이동 가능한 위치를 예측하며, 정합과정을 거쳐 이동물체의 이동 가능한 위치를 예측하며, 정합과정을 거쳐 예측위치에 대한 이동물체의 동일성 판별을 수행하게 된다.
* 정합기반 이동물체 추적기법은 전체적인 휘도 변화에 대한 적응능력이 좋으며, 배경과 위치의 변화가 발생할 경우에도 적용할 수 있다는 장점을 가지고있다.
* 그러한 추적대상의 프레임간의 변화가 클 경우 정합성능이 저하되고, 추적대상의 움직임이 고속인 경우 추적대상이 저주파 성분으로 이루어지기 때문에 정합을 위한 템플릿 추출에 어려움이 발생하게 된다.

에너지기반 이동물체 추적

* 광류, 능동외곽선, 레벨 셋 등과 같은 세부적인 분류가 있으며, 공통적으로 화소, 영역, 윤곽선 등과 같은 영상의 특징점이 프레임 간에서 에너지보존 법칙을 준수한다는가정을 기초로 한다.
* 즉, 짧은 시간 내에서 얻어지는 연속하는 두 프레임에 대하여 한 화소 또는 한 영역은 공간적인 변화만 존재하며, 밝기 값이나 분포, 즉 화소자체가 소유하고 있는 빛 에너지를 보존된다는 것이다.
* 이 기법은 계산량이 증가하지만 화면의 미세한 움직임까지 포착할 수 있으며, 추적 대상의 형태변화가 클 경우에도 강인간 추적 성능을 보여주는 장점을 가지고 있다.

---

[A Review on Object Detection and Tracking Methods
](https://ijrest.net/downloads/volume-2/issue-1/pid-21201506.pdf) : 2015

### [A Survey on Object Detection and Tracking Methods](https://pdfs.semanticscholar.org/25a6/c5dff9a7019475daa81cd5a7f1f2dcdb5cf1.pdf): 2014

![image](https://user-images.githubusercontent.com/17797922/40040388-0ac64296-5855-11e8-8b14-5b15cc508410.png)


* Tracking Methods
* Region-based tracking methods
* contour tracking methods
* 3D Model based tracking methods
* Feature based tracking methods
* Color and Pattern based tracking methods

> [Moving Object Tracking of Vehicle Detection”: A Concise Review](http://docplayer.net/16497156-Moving-object-tracking-of-vehicle-detection-a-concise-review.html): 2015


---

## pyimagesearch 소개 8개의 tracker

> [OpenCV Object Tracking](https://www.pyimagesearch.com/2018/07/30/opencv-object-tracking/), [[code_SingleOT]](https://gist.github.com/adioshun/779738c3e28151ffbb9dc7d2b13c2c0a), [[code_MOT]](https://gist.github.com/adioshun/72106c82674fd6cd7b06fe9105c2ab86)

OpenCV includes eight (yes, eight!) separate object tracking implementations

1. BOOSTING Tracker: Based on the same algorithm used to power the machine learning behind Haar cascades (AdaBoost), but like Haar cascades, is over a decade old. This tracker is slow and doesn’t work very well. Interesting only for legacy reasons and comparing other algorithms. (minimum OpenCV 3.0.0)

2. MIL Tracker: Better accuracy than BOOSTING tracker but does a poor job of reporting failure. (minimum OpenCV 3.0.0)

3. KCF Tracker: Kernelized Correlation Filters. Faster than BOOSTING and MIL. Similar to MIL and KCF, does not handle full occlusion well. (minimum OpenCV 3.1.0)

4. CSRT Tracker: Discriminative Correlation Filter (with Channel and Spatial Reliability). Tends to be more accurate than KCF but slightly slower. (minimum OpenCV 3.4.2)

5. MedianFlow Tracker: Does a nice job reporting failures; however, if there is too large of a jump in motion, such as fast moving objects, or objects that change quickly in their appearance, the model will fail. (minimum OpenCV 3.0.0)

6. TLD Tracker: I’m not sure if there is a problem with the OpenCV implementation of the TLD tracker or the actual algorithm itself, but the TLD tracker was incredibly prone to false-positives. I do not recommend using this OpenCV object tracker. (minimum OpenCV 3.0.0)

7. MOSSE Tracker: Very, very fast. Not as accurate as CSRT or KCF but a good choice if you need pure speed. (minimum OpenCV 3.4.1)

8. GOTURN Tracker: The only deep learning-based object detector included in OpenCV. It requires additional model files to run (will not be covered in this post). My initial experiments showed it was a bit of a pain to use even though it reportedly handles viewing changes well (my initial experiments didn’t confirm this though). I’ll try to cover it in a future post, but in the meantime, take a look at Satya’s writeup. (minimum OpenCV 3.2.0)


My personal suggestion is to:

- Use CSRT when you need higher object tracking accuracy and can tolerate slower FPS throughput

- Use KCF when you need faster FPS throughput but can handle slightly lower object tracking accuracy

- Use MOSSE when you need pure speed




---


## Tracking 수행 절차

> 자율 주행 차량의 다중 물체 추적 알고리즘, 이재준, 한국기술교육대학교, 2015

군집화시키고 각각의 군집들 을 추적(Tracking)하면 물체의 크기, 속도 등과 같이 더 많은 정보를 추출하는 것이 가능하다


본 논문에서 소개하는 물체 추적 알고리즘의 구성
- 데이터 군집화(Data Clustering)
- 데이터 관계 분석(Data Association)
- 상태 추정(State Estimation)
- 데이터 정리(Data Arrangement)


### 2.1 데이터 군집화(Data Clustering)

우선 데이터를 시간 순서대로 나열하여 생성된 2D Depth Image 내에서 지역 탐색을 이용하여 빠르게 군집화[1]를 수행한다


False separations 을 제거하기 위하여 군집들을 병합하는 단계를 추가로 수행
- 병합과정은 전역 탐색으로 이루어진다

```
[1] J. B. Trevor, S. Gedikli, R. B. Rusu, H. I. Christensen ,“Efficient Organized Point Cloud Segmentation with Connected Components,”
```

### 2.2 데이터 관계 분석(Data Association)

데이터 관계 분석은 **과거의 데이터**를 통해 **예측한 데이터**와 **새롭게 관측된 데이터**의 관계를 분석하는 단계이다.

관계 분석 과정에는 2 가지 중요한요소가 있다.
- 특징(Feature)의 선택
    - 일반적으로 위치 특징이 주로 특징 벡터로 사용되며 높이, 길이, 너비 등이 추가적인 특징으로 사용된다.
    - 하지만 LIDAR 의 특성상 때때로 길이, 너비등과 같은 특징은 움직이는 물체들에서 심하게 변동하는 특성을 보이기 때문에 위치와 높이만을 사용하였다.
- 할당(Assignment) 전략
    - 모든 군집과 추적 물체조합의 거리의 합을 근사적으로 최소화시키는 GNN(Global Nearest Neighbor)의 근사(Approximation)방식을 사용하였다.
    - 할당 전략은 군집-추적물체 테이블에서 가장 낮은 거리의 조합부터 차례대로 할당해 나가는 전략[2]을 취하였다.
    - 헝가리언 알고리즘을 적용 하기도 한다. [[상세]](https://cafe.naver.com/opencv/50555)

```
[2] F. Bourgeois and J. C. Lassalle, “An Extension of the Munkres Algorithm for the Assignment Problem to Rectangular Matrices.” Communications of the ACM, vol. 14, no. 12, p. 802, December, 1971.
```

[[추천] Introduction to Data Association](http://www.cse.psu.edu/~rtc12/CSE598C/datassocPart1.pdf): ppt, CSE598C Fall, 2012, Bob Collins, CSE, PSU

### 2.3 상태 추정(State Estimation)

상태 추정 과정은 데이터 관계 분석을 통해 얻은 대응 관계를 이용하여 측정값(군집)으로 그에대응하는 추적 물체의 상태를 갱신하는 단계이다.

상태 추정은 **등속 선형 운동 모델**을 가정하여 수행되었고 상태 추정 알고리즘으로는 **칼만 필터**를 사용하였다[4].

상태 벡터는 위치와 속도만으로 구성된다.

### 2.4 데이터 정리(Data Arrangement)

데이터 정리 과정에서는 불필요한 데이터의 삭제와 새로운 데이터의 등록이 이루어진다.

데이터의 등록은 새로운 물체가 나타나는 즉시 실행되지만 삭제는 시간 지연을 두고 실행되어 잡음, 가려짐(occlusion)등에 의해 물체가 센서의 시야에서 사라지는 현상에 더 강인하게 동작할 수 있도록 하였다.

하지만 때때로 이런 지연전략이 추적 물체 목록을 비대하게 만들 수 있기 때문에 상대적으로 관측 횟수가 적은 물체에는 더 작은 시간 지연을 부여하여 불필요한 리소스 소모를 줄였다.

---



## 4. Obstacle tracking

vehicle odometry 정보 추가적으로 활용

연속적으로 얻어지는 인식 결과를 바탕으로 이러한 오탐을 줄일 수 있는데, 이룰 추적기법(Tracking)이라고 한다.
- 이전 프레임의 포인트를 현재 프레임의 물체에 자동으로 누적하여 물체 해상도 및 보행자 분류 성능을 향상

### 4.1 단일 칼만 필터 기반

일반적으로 단일 객체 추적에 적용

Teichman의 연구[7]에선 단일 칼만 필터기반 추적기법을 이용하여 데이터를 누적시켜 분류의 성능을 높이고자 했다.

하지만 물체가 몇 개 없는 단조로운 시나리오에서 전후 프레임 간에 일치되는 물체관계를 이미 알고 있다고 가정하여, 특별한 데이터 연계 방법 없이 해당 물체 정보들을 단일 칼만 필터만 사용해추적 및 누적하여 포인트 수 증가를 유도하였다.

```
[7] A. Teichman, J. Levinson and S. Thrun, “Towards 3D Object Recognition via Classification of Arbitrary Object Tracks,” International Conference on Robotics and Automation, Shanghai, China, May 2011.
```

### 4.2 GM-PHD 필터

Data Associateion까지 고려한 다중 객체 추적에 적용

이전 프레임의 포인트를 현재 프레임의 물체에 자동으로 누적하여 물체 해상도 및 보행자 분류 성능을 향상

```
이연주, 서승우, "GM-PHD 필터를 이용한 보행자 탐지 성능 향상 방법", 서울대, 2015
```


---
