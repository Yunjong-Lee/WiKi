
# Index  

[1. FMCW Radar 개요](#1-FMCW-Radar-개요)  
[2. Doppler Effect](#2-Doppler-Effect)  
[3. Fast Fourier Transform](#3-Fast-Fourier-Transform)  
[4. Beamforming](#4-beamforming)  
[5. Steering Vector](#5-Steering-vector)


</br>

![](https://ogu45.com/zbxe/files/attach/images/96/027/074/ec649a91286d5c2e08dd54df08aa11d4.jpg)  

# 1. FMCW Radar 개요
- Rarget에 전송한 신호(송신 신호)와 반사되어 되돌아 오는 신호(수신 신호)의 추파수 라이를 이용하여 거리를 측정
- 송신 신호는 변조신호에 의해 선형적으로 변화
- 수신 신호는 $\tau_d(= 2R / c)$의 시간 차를 가지며, 송신 신호와 혼합됨(시간 차는 두 신호간 주파수 차이로 대체되며, 주파수 차이를 비트 주파수라 한다. 이 비트 주파수를 거리 측정에 이용)
- 비트 신호는 A/D를 거쳐 DMA를 통해 DSP로 전송(FFT를 통해 얻어진 비트스펙트럼에서 최대값을 찾아 거리로 환산)  
  + 송신신호와 수신신호의 차 주파수 계산
  + 선형성이 우수한 구간 선택
- FMCW 레이더의 성능
  + VCO의 Sweep 대역폭을 크게 할 수록 거리 해상도 개선(변조된 VCO의 출력주파수는 비선형 특성을 가지기 때문에 거리해상도를 개선시키는데 비용이 추가되어야 한다.)
  + 대안: Time Gating 방법(DSP) 등이 제시 됨  

</br>  

# 2. Doppler Effect  
- 21.12.10  

# 2.1. 정의  
음파 또는 전파의 발생지/수신지가 다가오거나 멀어짐에 따라 수신 주파수가 변화하는 현상  
: 발생점,관측점이 다가올 때 → 수신 주파수가 높아짐  
: 발생점,관측점이 멀어질 때 → 수신 주파수가 낮아짐  

# 2.2. 관계식  
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
       . $f_r$ : 수신 주파수, v : 이동체 접근 속도, c : 빛 속도, $f$ : 송신 주파수  

  - 도플러 효과 관계식 - 2차원 평면 관계 (각도 고려 필요)  
    : 이동 파원, 정지 관측자 일 때,   
     ![img](http://www.ktword.co.kr/img_data/2621_5.jpg)  
     -  t > 0 : 파원 속도가 양수 즉, 파원이 멀어짐  
     -  t < 0 : 파원 속도가 음수 즉, 파원이 가까워짐  

  - 이동 무선 채널 상의 도플러 효과  
    : 이동 무선단말의 도플러 효과에 따른 주파수 천이량  ☞ 도플러 천이(Doppler Shift) 참조  
    : 무선단말 이동에 따른 도플러 효과에 의해 주파수 변동 특성  ☞ 도플러확산 참조  
     - 다중경로 채널의 시변(時變) 특성 => 도플러 확산 (Doppler Spread) 또는 주파수 분산 초래  
  
# 2.3. 도플러 효과에 의한 주파수 변동  
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
    - 

</br>

---

# 3. Fast Fourier Transform  
- 22.01.21  
- [23.08.22](https://download.ni.com/evaluation/pxi/Understanding%20FFTs%20and%20Windowing.pdf)
  
# 3.1. DFT  

$X[k] = x[0](W_N)^0 + x[1](W_N)^k + ... + x[n-1](W_N)^(n-1)k, (k = 0, 1, ~ n-1)$  
  
  - $W_N^(n-1)$ : 회전인자 (twiddle factor, 복소지수함수의 간결한 표현)  
  - $x_k$ 하나의 계산은 n개의 $x_k$ 데이터를 이용하여 n개 항의 곱셈 및 (n-1)개의 덧셈 필요  
  - k가 n개 점을 나타내므로, n개의 $x_k$ 계산 필요 (n-point DFT 계산은 $n^2$ 번의 복소수 곱셈 계산 필요, n이 증가할수록 계산량이 n배수 만큼 증가됨)
  - 회전인자 관련 계산 항의 수 : $0 < kn <= (n-1)^2$
    + 회전인자의 대칭성 및 주기성을 이용하여 계산량을 줄일 수 있음. 단위 원을 한바퀴 도는데 필요한 서로 다른 N개의 값만 계산  

# 3.2. FFT 
DFT의 상수 및 동작의 대칭성을 이용하여 계산량을 감소  
- DFT를 길이가 짧은 여러 DFT로 계속 분할시켜 곱셈 량을 N에 비례하도록 함  
  . $x_n$을 짧은 길이의 신호로 분할
  . 분할된 신호의 DFT를 각각 계산
  . 각 DFT 결과를 결합하여 $X_k$ 계산
- n-point FFT 계산 : nlog_2n에 비례

- [주요 파라미터](http://www.ktword.co.kr/test/view/view.php?m_temp1=2596&id=1276)
- [FFT 알고리듬 분류](http://www.ktword.co.kr/test/view/view.php?m_temp1=2596&id=1276)


# 3.3. window function  

[불연속에 의한 스펙트럼의 왜곡을 막기 위한 방법으로, 데이터에 "컨볼루션 연산을 하는 방법"과 "window function을 곱하는 방법"이 있다](https://paeton.tistory.com/entry/Window-Function%EC%9D%84-%EC%93%B0%EB%8A%94-%EC%9D%B4%EC%9C%A0)

## 3.3.1. 데이터에 컨볼루션
  - 윈도우 함수 자체를 하나의 filter로 사용(대부분의 window function은 주파수축에서 low-pass filter형태)되며, 신호 자체가 smoothing 된다.  
    + $s'(t)=s(t)\ast w(t)$   

## 3.3.2. 데이터에 window function을 곱셈(시간축에서 신호에 윈도우를 곱했음)
  - 시간축에서의 곱셈은 주파수 축에서의 컨볼루션(퓨리에변환)  
    + 주파수축의 스펙트럼을 filtering  
      - $*$ s'(t)=s(t)\cdot w(t) $*$  
      - $*$F\left\{ s'(t) \right\} =F\{ s(t)\cdot w(t)\} =F\{ s(t)\} \ast F\{ w(t)\} $*$  

  - 긴(길이) 연속 신호 처리를 위해 블럭(프레임) 단위로 나눔  
    + 신호 복원시 블럭의 양끝에서 신호의 불연속을 막거나 주파수 스펙트럼의 왜곡을 막기 위해 윈도우(블럭)를 씌움  
    + 종류
      - Rectangular : 신호를 말그대로 블럭으로 나누는 것, 다른 윈도우는 블럭 경계로 갈수록 크기가 작아지는 함수		
	+ Rectangular 윈도우의 경우 양끝에서 신호의 불연속이 있기 때문에 스펙트럼 상에서 인접 주파수 성분으로 smearing된다.
      - Hamming   : 음성신호처리에서는 Hamming 윈도우가 side lobe의 attenuation이 크고 main lobe의 폭도 좁아서 자주 사용된다.  
	+ 블럭으로 나누어진 신호와 원래 신호의 스펙트럼 차이가 rectangular window보다 작다. 
	+ 윈도우 함수의 길이(프레임 길이)는 음성 신호의 특징과 관련  
    + 음성신호는 음소의 나열이며, 음소의 길이는 무성음은 30-50 ms, 유성음은 50-200 ms 정도,   
      - 유성음은 피치 주기 단위로 거의 유사한 신호가 반복(피치_min: 80Hz, 피치 주기_max: 12.5 ms).
      - 최소한 하나의 피치 주기가 들어가고 거의 stationary한 신호를 포함하기 위하여 대략 20-30 ms를 프레임의 크기로 정합니다.
      - 이보다 작은 프레임 크기를 사용하면 한 피치 주기보다 짧은 음성신호만을 포함할 수 있으며, 프레임 길이가 더 길어지면
        한 프레임내에 서로 다른 음소 부분이 혼합되는 경우가 자주 발생하여 음성신호의 특징을 제대로 표현할 수가 없습니다.
      - Hanning  
	
# 3.4. [푸리에 급수](https://ogu45.com/zbxe/school/74027)
  - 정현파를 이용하여 신호의 표현을 찾는 문제  
    + 주기 신호를 주파수가 서로 다른 정현파의 합으로 나타낼 수 있음(푸리에, Fr) → 푸리에 해석이라고 한다.  
    + 주기 신호는 그 신호와 같은 주기를 갖는 정현파와 이 정현파의 정수배의 주파수를 갖는 정현파들의 합으로 표현할 수 있다. 이 때 주기 신호와 주기(T)가 같은 정현파를 기본파(fundamental wave)라고 하고 이 정현파의 주파수 $f_0 = \frac{1}{T} \lbrace\omega_0 = \frac{2\pi}{T} \rbrace$를 기본 주파수(fundamental period)라 한다.  
    + 또, $kf_0(k\omega_0, k=2,3,4, ⋯ )$의 주파수를 갖는 정현파를 k고조파(harmonics, 기본파의 주파수의 정수배 주파수를 갖는 정현파)라고 한다.  
    + 몇 개의 정현파의 합으로 표현되는 주기 신호도 있지만, 보통 많은 수(경우에 따라서는 무한개)의 정현파가 필요한 주기 신호도 있다. 푸리에의 결과를 일반화하여 수식으로 나타내면
      >  $x(t) = DC + f_w(cos+sin)+f_h(cos+sin) $  
      >  $a_0 + \displaystyle\sum_{k=1}^{ \infty} a_k cosk\omega_0 t + \displaystyle\sum_{k=1}^{ \infty} b_k sin\omega_0 t + \cdots $  
    + 이와 같이 주기 신호를 기본파와 고조파들의 합으로 나타낸 식을 푸리에 급수라고 한다.  
    + 주기 신호를 위의 식과 같이 표현하려면 푸리에 계수라고 하는 각 항의 계수 $a_0, a_k, b_k$를 구해야 하는데, 정현파 신호의 직교성을 이용하여 구할 수 있다.  
      > $a_0 = \frac{1}{T} \int_T x(t) \mathrm{d}t$  
      > $a_k = \frac{2}{T} \int_T x(t)cosk\omega_0 t \mathrm{d}t$
      > $b_k = \frac{2}{T} \int_T x(t)sink\omega_0 t \mathrm{d}t$  

  - 푸리에 급수는 주기 신호가 기본 주파수의 정수배가 되는 주파수 성분만 가지는 것이 성립하기 위해서는 푸리에 급수가 수렴해야하며, 수렴에 관한 조건을 정리한 것이 Dirichlet(디리클레) 조건이다.
    > - 신호의 한 주기 내에서 $x(t)$는 적분가능해야 한다.  
        + $\int_T |x(t)| \mathrm{d}t$  
    > - 신호의 한 주기 내에 존재하는 극대 극소점의 수는 유한해야 한다.  
    > - 신호의 한 주기 내에 존재하는 불연속점의 수는 유한해야 한다.  

  - 진폭 스펙트럼의 역할
    + 진폭 스펙트럼은 신호가 갖는 다양한 주파수 성분의 양(정현파 진폭)을 나타내며, 저주파에서 고주파로 갈수록 값이 감소하는 특성을 가짐.
    + 파형의 시간적인 변화가 완만한 신호의 진폭은 스펙트럼의 감소가 급격히 일어나고, 반대로 시간적으로 급격한 변화를 보이는 신호의 진폭 스펙트럼 감소는 완만하다.
      > - 파형 변화가 급하지 않고 비교적 매끄러운 신호라면, 신호의 대략적인 모양을 만들어주는 몇 개의 두드러진 저주파수 정현파와 세부적인 변화를 맞추어주는 작은 값의 고주파수 정현파들만으로 신호를 만들 수 있다. 이 때문에 진폭 스펙트럼은 주파수 증가에 따라 빠르게 감쇠한다. 따라서 적은 수의 푸리에 급수 항으로도 양호하게 근사적으로 합성할 수 있다. 극단적인 예로 정현파의 경우에는 기본 주파수 $ω_0$ 에서만 진폭 스펙트럼의 값이 나타난다. </br>
      > - 반면에, 불연속점을 갖는 사각 펄스와 같이 급격한 변화를 포함하는 신호는 이를 구현하기 위해 많은 주파수 성분이 필요할 뿐 아니라 고주파 성분의 크기도 상대적으로 무시할 수 없는 값을 갖는다. 따라서 진폭 스펙트름은 주파수에 따라서 느리게 감쇠할 것이고, 신호를 근사적으로 합성할 때 오차를 작게 하려면 많은 수의 푸리에 급수 항이 필요하다.  </br>

    + 사각 펄스 신호는 푸리에 급수로 전개하면 무한개의 주파수 성분을 가진다. [그림. 주파수 합성에 의한 사각 펄스 신호의 근사화]은 스펙트럼에 존재하는 고조파들을 차례로 더하여 사각 펄스 신호를 합성하는 과정을 보인 것이다. 그림에서 보면 세 개의 고조파만 더해져도 사각 펄스와 비슷한 모양을 갖추지만, 아직 불연속점의 날카로운 모서리가 이 합성 신호에는 나타나지 않는다. 왜냐하면 날카로운 모서리를 구현하기 위해서는 급격히 변하는 (고주파수)성분이 필요하기 때문이다. 고조파의 수를 점진적으로 늘림에 따라 모서리는 서서히 날카로워지며 신호는 사각 펄스에 더욱 가까워진다.  
      ![](https://ogu45.com/zbxe/files/attach/images/96/027/074/4e5bdc8db5ce58d73d9478fe90cab1be.jpg)  
      > 고조파의 수를 늘려가도 불연속점 부근에서 오버슈트가 생기며 파형이 평탄하지 않고 진동하는 현상을 관찰할 수 있다. 이론적으로는 무한개의 고조파를 더하면 정확히 사각펄스가 되어야 하지만, 실제 고조파 합성 신호는 고조파의 수를 아무리 늘리더라도 불연속점 근처에서 항상 불연속 크기의 약 9%의 오버슈트가 생기며, 고조파수에 비례하여 진동도 더 빨라진다. 이러한 현상을 Gibbs 현상이라고 한다.  </br>
      
  - 위상 스펙트럼의 역할
    + 각 주파수 성분의 시간축 상의 위치를 표시한다. 진폭 스펙트럼이 같더라도 위상 스펙트럼이 다르면 신호의 파형이 달라짐
      ![](https://ogu45.com/zbxe/files/attach/images/96/027/074/8a9065f701a67c0c0bc43b473586bbb1.jpg)  
    
  - 

 
  - 


  
</br>

# 4. Beamforming

</br>

# 5. Steering vector
- 안테나 배열에서 발생하는 위상차로, 입사각과 안테나 사이의 거리(r)에 의해 정의할 수 있다.
- doppler freq.를 나타내는 vctor와 안테나의 고도각과 방위각을 나타내는 vector의 외적에 의해 형성됨



---  

[3] S. He and M. Torkelson, “A new approach to pipelined FFT processor”, IPPS’96, pp.766-770, 1996.  
[4] J. Y. Oh and M. S. Lim, “New radix-2 to the 4th power pipeline FFT processor”, IEICEtrans. Electron., vol. E88-C, no. 8, pp.1740-1746, 2005.  
[5] T. S. Cho and H. H. Lee, “A high-speed low-complexity modified radix-2^5 FFT processor for high rate WPAN applications”, IEEE Trans. Very Large Scale Integr. (VLSI) Syst, vol. 21, no. 1, pp. 187-191, Feb, 2013.  
[6] C. Yang, C. Wei, Y. Xie, H. Chen and C. Ma, “Area-efficient mixed-radix variable-length FFT processor”, IEICE Electron. Expr., vol. 14, no. 10, pp. 1-10, 2017. 
[7] S. J. Huang, S. G. Chen, “A high-throughput radix-16 FFT processor with parallel and normal input/output ordering for IEEE 802.15. 3c systems”, IEEE Tran. Circuits Sys. I: Reg. Papers, vol. 59, no. 8, pp.1752-1765, 2012.  




