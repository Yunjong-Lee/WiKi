
# Index
1. [Fast FOurier Transfrm](# Fast-FOurier-Transfrm)
2. [Doppler Effect](# Doppler-Effect)



# Doppler effect
- 21.12.10

## 정의  
음파 또는 전파의 발생지/수신지가 다가오거나 멀어짐에 따라 수신 주파수가 변화하는 현상  
: 발생점,관측점이 다가올 때 → 수신 주파수가 높아짐  
: 발생점,관측점이 멀어질 때 → 수신 주파수가 낮아짐  

## 관계식  
  - 도플러 효과 관계식 - 1차원 직선 관계  
    : 이동 파원, 이동 관측자 일 때,  
     ![img](http://www.ktword.co.kr/img_data/2621_4.JPG)  

    : 정지 파원, 이동 관측자 일 때,  
  ![img](http://www.ktword.co.kr/img_data/2621_2.jpg)  
     
    : 이동 파원, 정지 관측자 일 때,  
  ![img](http://www.ktword.co.kr/img_data/2621_3.JPG)
     
  ※ 빛과 같은 전자기파는 상대론적 고려가 있을 경우 다른 관계식을 따름  
     - 광속은 광원,관측자 이동에 무관하게 일정함  
     ![img](http://www.ktword.co.kr/img_data/2621_1.JPG)  
       . fr : 수신 주파수, v : 이동체 접근 속도, c : 빛 속도, f : 송신 주파수  

  - 도플러 효과 관계식 - 2차원 평면 관계 (각도 고려 필요)  
    : 이동 파원, 정지 관측자 일 때,  
     ![img](http://www.ktword.co.kr/img_data/2621_5.jpg)  
     -  t > 0 : 파원 속도가 양수 즉, 파원이 멀어짐  
     -  t < 0 : 파원 속도가 음수 즉, 파원이 가까워짐  

  - 이동 무선 채널 상의 도플러 효과  
    : 이동 무선단말의 도플러 효과에 따른 주파수 천이량  ☞ 도플러 천이(Doppler Shift) 참조  
    : 무선단말 이동에 따른 도플러 효과에 의해 주파수 변동 특성  ☞ 도플러확산 참조  
     - 다중경로 채널의 시변(時變) 특성 => 도플러 확산 (Doppler Spread) 또는 주파수 분산 초래  
  
2. 도플러 효과에 의한 주파수 변동  
  - 정의  
    . 도플러 천이 (Doppler Shift, Frequency Shift): 무선통신에서 도플러 효과(Doppler Effect)에 따른 겉보기 주파수의 천이/편이  
    . 도플러 주파수 옵셋 (Doppler Frequency Offset): 레이더 등에서의 송신,수신 주파수 간의 차이/편차  

  - 이동 무선단말의 도플러 천이(Doppler Shift, Frequency Shift) 근사 관계식  
    . 이동에 따른 도플러 효과에 의한 겉보기 수신 주파수의 변동 측도(measure)  
      - 도플러 천이는 이동체의 속도, 수신전파 주파수, 전파도래각도(AoA)와 관련됨  
        . θ = 0˚  (전파방향과 반대)  
           ..  fD = (+) (v f / c)  = (+) (v / λ)  
        . θ = 90˚ (전파방향과 수직)  
           ..  fD = 0  
        . θ = 180˚(전파방향과 같음)   
           ..  fD = (-) (v f / c)  = (-) (v / λ)  

    - 도플러 천이(주파수 천이)는 이동방향이 전파방향과 반대면 양(+)/같은 방향이면 음(-)/수직이면 거의 변화없음  

  - 최대 도플러 주파수 천이 근사식 (cos 0˚ = 1)  
    - fDmax : 최대도플러주파수천이, v :이동 속도, c : 빛 속도, fo: 전송 주파수  
    - 최대 도플러 천이는, 전송 주파수 및 이동 속도가 커질수록 커지게 됨 

---

# Fast Fourier Transform  
- 22.01.21  

## DFT
 
	X[k] = x[0](W_N)^0 + x[1](W_N)^k + ... + x[n-1](W_N)^(n-1)k, (k = 0, 1, ~ n-1)  
	
	- (W_N)^(n-1) : 회전인자 (twiddle factor, 복소지수함수의 간결한 표현)  
	- x[k] 하나의 계산은 n개의 x[k] 데이터를 이용하여 n개 항의 곱셈 및 (n-1)개의 덧셈이 필요함  
	- k가 n개 점을 나타내므로, n개의 x[k] 계산이 필요 (n-point DFT 계산은 n^2 번의 복소수 곱셈 계산 필요, n이 증가할수록 계산량이 n배수 만큼 증가됨)  
	- 회전인자 관련 계산 항의 수 : 0 < kn <= (n-1)^2  
	  + 회전인자의 대칭성 및 주기성을 이용하여 계산량을 줄일 수 있음. 단위 원을 한바퀴 도는데 필요한 서로 다른 N개의 값만 계산  

## FFT 
DFT의 상수 및 동작의 대칭성을 이용하여 계산량을 감소  
- DFT를 길이가 짧은 여러 DFT로 계속 분할시켜 곱셈 량을 N에 비례하도록 함  
  . x[n]을 짧은 길이의 신호로 분할
  . 각 분할된 신호의 DFT를 각각 계산
  . 각 DFT 결과를 결합하여 X[k] 계산
- n-point FFT 계산 : nlog_2n에 비례

- [주요 파라미터](http://www.ktword.co.kr/test/view/view.php?m_temp1=2596&id=1276)
- [FFT 알고리듬 분류](http://www.ktword.co.kr/test/view/view.php?m_temp1=2596&id=1276)


## window function  

[불연속에 의한 스펙트럼의 왜곡을 막기 위한 방법으로, 데이터에 컨볼루션 연산을 하는 방법과 데이터에 window function을 곱하는 방법이 있다](https://paeton.tistory.com/entry/Window-Function%EC%9D%84-%EC%93%B0%EB%8A%94-%EC%9D%B4%EC%9C%A0)

  ### 데이터에 컨볼루션
  윈도우 함수 자체를 하나의 filter로 사용(대부분의 window function은 주파수축에서 low-pass filter형태)되며, 신호 자체가 smoothing 된다.  
    + $*$ s'(t)=s(t)\ast w(t) $*$   
  ### 데이터에 window function을 곱셈(시간축에서 신호에 윈도우를 곱했음)
  시간축에서의 곱셈은 주파수 축에서의 컨볼루션(퓨리에변환)  
      └─ 주파수축의 스펙트럼을 filtering  
    + $*$ s'(t)=s(t)\cdot w(t) $*$  
	   + $*$F\left\{ s'(t) \right\} =F\{ s(t)\cdot w(t)\} =F\{ s(t)\} \ast F\{ w(t)\} $*$  

  - 긴(길이) 연속 신호 처리를 위해 블럭(프레임) 단위로 나눔  
    : 신호 복원시 블럭의 양끝에서 신호의 불연속을 막거나 주파수 스펙트럼의 왜곡을 막기 위해 윈도우(블럭)를 씌움  
        └─ 종류	  
		+ Rectangular : 신호를 말그대로 블럭으로 나누는 것, 다른 윈도우는 블럭 경계로 갈수록 크기가 작아지는 함수		
				- Rectangular 윈도우의 경우 양끝에서 신호의 불연속이 있기 때문에 스펙트럼 상에서 인접 주파수 성분으로 smearing된다.  
		+ Hamming   : 음성신호처리에서는 Hamming 윈도우가 side lobe의 attenuation이 크고 main lobe의 폭도 좁아서 자주 사용된다.  
		  - 블럭으로 나누어진 신호와 원래 신호의 스펙트럼 차이가 rectangular window보다 작다. 
		  - 윈도우 함수의 길이(프레임 길이)는 음성 신호의 특징과 관련  
    - 음성신호는 음소의 나열이며, 음소의 길이는 무성음은 30-50 ms, 유성음은 50-200 ms 정도,   
			유성음은 피치 주기 단위로 거의 유사한 신호가 반복(피치_min: 80Hz, 피치 주기_max: 12.5 ms).   
			최소한 하나의 피치 주기가 들어가고 거의 stationary한 신호를 포함하기 위하여  
			대략 20-30 ms를 프레임의 크기로 정합니다.  
			이보다 작은 프레임 크기를 사용하면 한 피치 주기보다 짧은 음성신호만을 포함할 수 있으며,  
			프레임 길이가 더 길어지면 한 프레임내에 서로 다른 음소 부분이 혼합되는 경우가 자주 발생하여  
			음성신호의 특징을 제대로 표현할 수가 없습니다.  
		+ Hanning  



---  

[3] S. He and M. Torkelson, “A new approach to pipelined FFT processor”, IPPS’96, pp.766-770, 1996.  
[4] J. Y. Oh and M. S. Lim, “New radix-2 to the 4th power pipeline FFT processor”, IEICEtrans. Electron., vol. E88-C, no. 8, pp.1740-1746, 2005.  
[5] T. S. Cho and H. H. Lee, “A high-speed low-complexity modified radix-2^5 FFT processor for high rate WPAN applications”, IEEE Trans. Very Large Scale Integr. (VLSI) Syst, vol. 21, no. 1, pp. 187-191, Feb, 2013.  
[6] C. Yang, C. Wei, Y. Xie, H. Chen and C. Ma, “Area-efficient mixed-radix variable-length FFT processor”, IEICE Electron. Expr., vol. 14, no. 10, pp. 1-10, 2017. 
[7] S. J. Huang, S. G. Chen, “A high-throughput radix-16 FFT processor with parallel and normal input/output ordering for IEEE 802.15. 3c systems”, IEEE Tran. Circuits Sys. I: Reg. Papers, vol. 59, no. 8, pp.1752-1765, 2012.  




