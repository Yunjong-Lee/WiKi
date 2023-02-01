# Radar 상호간섭  

### '[차량용 레이더 간섭신호에 대한 영향성 연구](https://webcache.googleusercontent.com/search?q=cache:8b7MFV-UdF4J:https://ettrends.etri.re.kr/ettrends/79/0905000399/18-1_033_041.pdf+&cd=7&hl=ko&ct=clnk&gl=kr)', 2019 한국자동차공학회 추계학술대회  

- 상호간섭 신호  
  + 정의 : 다른 차량에 장착된 레이더에서의 송신 신호가 자가 차량의 레이더에 수신되어 실제 표적 검출을 방해하는 신호  
  + 제거 : Constant False Alarm Rate 레벨 조정  
  
- 모델  
  + 간섭 신호 모델링 : 간섭신호의 영향으로 doppler bin과 range bin에서 평균 잡음 레벨보다 큰 신호를 표적으로 검출될 수 있음  
    + 간섭신호의 주파수 대역폭(BW)은 다르고 동일한 시간 주기(PRI)를 가지는 경우
      : 1D FFT의 잡음 레벨이 일정하게 올라가며 2D FFT에서 여러 doppler bin에서 range bin에 대해 검출됨  
    + 간섭신호의 BW은 같고 PRI가 다를 경우
      : 간섭신호는 주파수 대역에서 넓게 퍼지는 현상이 발생(1D FFT의 잡음 레벨을 일정하게 높임)  
      : CFAR 알고리즘의 문턱값을 (증가한 잡음 레벨만큼) 올리면 간섭 영향 없이 실제 표적 구분 가능  
 
- 용어
  + 도플러 주파수 : 해당 물체의 움직임을 추정할 때 활용되는 값  
  + doppler bin  
  + range bin  
  + CFAR : 수신신호의 잡음 레벨을 계산하여 잡음, 클러터, 간섭 등의 영향에 대응하여 표적을 감지하는 역할  


---


### [Range Doppler Detection for automotive FMCW Radars](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=4405477)
- Ref : Proceedings of the 37th European Microwave Conference, infineon technology   

- tx와 rx 신호간의 difference는 downconversion 후에 결정  
  하나의 주파수 램프에서 추출된 정보로부터 range와 velocity를 함께 검출하는 것은 불완전하다. 불완전을 제거하기 위해 후속 램프들을 생성해야 한다.  
  
- range와 velocity 추출 method  
  + FFT
  + CFAR  
  
- HW 구성
  + Frequency : 24 GHz, sweep bandwidth B = 1 GHz 
  + Front-End (TSLP-16-Package)  
    + tx : VCO & 2 output buffer(deficated for LO Disrtibution & tx antenna)
    + rx : 2 receive path (for angle detection, in parallel), LNA, Mixer, ADC

- radar equation  
  + The basic idea in FMCW에서 기본 개념은 'linear frequency ramp' 생성  
    - bandwidth B와  [-T/2 ~ T/2] 사이의 주기 T를 가지는 하나의 램프에 대한 전송주파수는  
![](https://latex.codecogs.com/gif.latex?f_t%20%28t%29%20%3D%20f_c%20&plus;%20%5Cfrac%7BB%7D%7BT%7Dt)   

  + phase ![](https://latex.codecogs.com/gif.latex?%5Cvarphi%20_t%28t%29) of tx signal ![](https://latex.codecogs.com/gif.latex?cos%28%5Cvarphi%20_t%28t%29%29) becomes after intrgration:  
![](https://latex.codecogs.com/gif.latex?%5Cvarphi%20_t%28t%29%20%3D%202%5Cpi%20%5Cint_%7B-T/2%7D%5E%7Bt%7Df_T%28t%29dt%20%5C%5C%20%3D%202%5Cpi%28f_ct&plus;%5Cfrac%7B1%7D%7B2%7D%5Ccdot%20%5Cfrac%7BB%7D%7BT%7Dt%5E2%29%7C_%7B-T/2%7D%5E%7Bt%7D%20%5C%5C%20%3D%202%5Cpi%28f_ct&plus;%5Cfrac%7B1%7D%7B2%7D%5Ccdot%20%5Cfrac%7BB%7D%7BT%7Dt%5E2%29%20-%20%5Cvarphi%20_t_0)  
- phase of the downconverted signal ![img](https://latex.codecogs.com/gif.latex?%5CDelta%5Cvarphi%28t%29%20%3D%20%5Cvarphi_T%28t%29%20-%20%5Cvarphi_T%28t-%5Ctau%29) is  
![img](https://latex.codecogs.com/gif.latex?%5CDelta%5Cvarphi%28t%29%20%3D%202%5Cpi%28f_c%5Ctau%20&plus;%20%5Cfrac%7BB%7D%7BT%7Dt%5Ctau%20-%20%5Cfrac%7BB%7D%7B2T%7D%5Ctau%5E2%29)  
where, ![img](https://latex.codecogs.com/gif.latex?%5Ctau) is the delay between the tx and rx signal of one target and last term in the equation can be neglected because ![img](https://latex.codecogs.com/gif.latex?%5Ctau/T%20%5Cll%201).  
For calculation of the delay(![img](https://latex.codecogs.com/gif.latex?%5Ctau)) is ![img](https://latex.codecogs.com/gif.latex?2%28R&plus;%5Cupsilon%20%5Ccdot%20t%29/c) a target at distance R with constant velocity (![img](https://latex.codecogs.com/gif.latex?%5Cupsilon)) is assumed.  
tihs leads to 
![img](https://latex.codecogs.com/gif.latex?%5CDelta%20%5Cvarphi%28t%29%20%3D%202%5Cpi%5Cleft%20%5B%20%5Cfrac%7B2f_cR%7D%7Bc%7D%20&plus;%20%28%5Cfrac%7B2f_c%20%5Ccdot%20%5Cupsilon%20%7D%7Bc%7D%20&plus;%20%5Cfrac%7B2B%20%5Ccdot%20R%7D%7BT_c%7D%29t%20&plus;%20%5Cfrac%7B2B%20%5Ccdot%20%5Cupsilon%20%7D%7BT%20%5Ccdot%20c%7Dt%5E2%20%5Cright%20%5D)  
The last term is called Range-Doppler-Coupling and can be neglected again 
![img](https://latex.codecogs.com/gif.latex?%5CDelta%20%5Cvarphi%28t%29%20%3D%202%5Cpi%5Cleft%20%5B%20%5Cfrac%7B2f_cR%7D%7Bc%7D%20&plus;%20%28%5Cfrac%7B2f_c%20%5Ccdot%20%5Cupsilon%20%7D%7Bc%7D%20&plus;%20%5Cfrac%7B2B%20%5Ccdot%20R%7D%7BT_c%7D%29t%20%5Cright%20%5D)  

The generated frequency is therefore 
![img](https://latex.codecogs.com/gif.latex?f_I_F%20%3D%20%5Cfrac%7B2f_c%20%5Ccdot%20%5Cupsilon%20%7D%7Bc%7D%20&plus;%20%5Cfrac%7B2B%20%5Ccdot%20R%7D%7BT_c%7D)  
  
rx signal (![img](https://latex.codecogs.com/gif.latex?S_I_F%20%3D%20cos%28%5CDelta%20%5Cvarphi%20%28t%29%29)) is sampled with an interval ![img](https://latex.codecogs.com/gif.latex?T_A), the samples are multiplied with a window function ![img](https://latex.codecogs.com/gif.latex?w%28n%29) and a zero padding is performed before FFT with the resulting samples is done.  
스펙트럼은 입력 신호가 실수(real)이기 때문에 대칭이다. 복소 기저대역 (complex baseband) signal는 ![img](https://latex.codecogs.com/gif.latex?s_I_F%28t%29%20&plus;%20i%20%5Ccdot%20H%20%5C%7B%20s_I_F%28t%29%20%5C%7D) 로 얻을 수 있다.  
![img](https://latex.codecogs.com/gif.latex?H%20%5C%7B%20...%20%5C%7D)는 Hilbert transformation을 나타냄  
![img](https://latex.codecogs.com/gif.latex?s_B%28n%29%20%3D%20A%20%5Ccdot%20w%28n%29e%5E%7Bi%20%5Ccdot%202%20%5Cpi%5B%5Cfrac%7B2f_cR%7D%7Bc%7D%20&plus;%20%28%5Cfrac%7B2f_c%20%5Ccdot%20v%7D%7Bc%7D%20&plus;%20%5Cfrac%7B2BR%7D%7BT_c%7D%29T_An%5D%7D) 
