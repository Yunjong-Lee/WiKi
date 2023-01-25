# Markdown 문법
[ref](https://eungbean.github.io/2018/06/11/How-to-use-markdown/)  


---

# Index

[1. 킨띄우기](#1-칸-띄우기)  
[2. 형광색 처리](#2-형광색-처리)  
[3. 코딩 블록 입히기](#3-코딩-블록-입히기)  
[4. 간트차트]()  
[5. Diagram 구문](#Diagram-구문)
  
--- 


### Diagram 구문
[Ref](https://mermaid.js.org/syntax/flowchart.html)  
##### 1. node and direction  
  - TD or TB : Top to bottom
  - BT : Buttom to top
  - LR : Left to right
  - RL : Right to Left

```mermaid
---
title: Node
---
flowchart TD
    start-->stop
```

##### 2. Node shapes
```mermaid
flowchart LR
  id1(Rectangle_box)
  id2[[box]]
  id3[(cylindrical shape, Database)]
  id4((circle))
  id5>asymmetric shape]
  id6{rhombus}  
  id7{{hexagon}}
  id8[/Parallelogram/]
  id9[\Parallelogram\]
  A[/Christmas\]
  B[\Go shopping/]
  C(((double circle)))
```  

##### 3. Flowchart
###### 3.1.
```mermaid
  flowchart LR
    A-->B
    B-->C
    C-->D
    D-->E
    click A "https://www.github.com" _blank
    click B "https://www.github.com" "Open this in a new tab" _blank
    click C href "https://www.github.com" _blank
    click D href "https://www.github.com" "Open this in a new tab" _blank
```  
###### 3.2.
```mermaid
  flowchart LR
    subgraph Case_01
      B1 --> B2
    end
    A --> Case_01 --> B
```
###### 3.3.
```mermaid
  flowchart LR
    subgraph TOP
      direction TB
      subgraph B1
          direction RL
          i1 -->f1
      end
      subgraph B2
          direction BT
          i2 -->f2
      end
    end
    A --> TOP --> B
    B1 --> B2
```



##### 4. [Graph](https://richwind.co.kr/147)
###### case_1  
```mermaid
  graph LR
A(입력)-->B[연산]
B-->C(출력)
```

###### Case_2
```mermaid
  graph
    A[X-Mas] -->|Get Money| B(Go Shopping)
    B --> C{Decision}
    C -->|01| D[Laptop]
    C -->|10| E[iPhone]
    C -->|11| F[fa:fa-car Car]
```

##### 5. Sequence Diagram  
```mermaid
%% Example of sequence diagram
  sequenceDiagram
    Alice->>Bob: Hello Bob, how are you?
    alt is sick
    Bob->>Alice: Not so good :(
    else is well
    Bob->>Alice: Feeling fresh like a daisy
    end
    opt Extra response
    Bob->>Alice: Thanks for asking
    end
```

##### 6. [class Diagram](https://mermaid.live/edit#pako:eNptkslOwzAQhl8l8glEF5pAl4gLoq3EoafeUCQ0sSeJVS_FC1UpfXec0IYu-OKZb_yPxzPeEaoZkpRQAdZOOZQGZKaisJ4VlyCip-9uN5p6urqmc26ra_qGuYEznEZ3XLkISrzES2e4KqMSFUNzGqwldgEymDe3FwEJDo-wKbspb_cLojZpjrB60UKbNmA3XB6Fwf3wQFdHf3-ar35Ym69b1275F76qOaJrMQU1A_evvmnBX0G51iLi9n3DBWuh8arVkg6RaCRwFibR6DLiKpSYkTSYDAvwwmUkU_VR8E4vt4qS1BmPHeLXLHTkMLtzOGPcaUPSAoQNUGgIfSbpjrjtup56ya0LGalWBS9r7o0IuHJubdN-vw73Su4qn_eoln3LWQXGVZ-TYX8YD8cQJzgcJfCYJIzmg8m4iB8GBRvdD2Ig-32HYHP_4vDF6m3_A4gUwp0)
```mermaid
  classDiagram
    Animal <|-- Duck
    Animal <|-- Fish
    Animal <|-- Zebra
    Animal : + int age
    Animal : + String gender
    Animal : +isMamal()
    Animal : +mate()
    class Duck{
      +String beakColor
      +swim()
      +quack()
    }
    class Fish{
      -int sizeInFeet
      -canEat()
    }
    class Zebra{
      +bool is_wild
      +run()
    }
```


##### 7. [state Diagram](https://mermaid.live/edit#pako:eNpdkDFvgzAQhf8KurGCEKAlCUOXJmOmjKXDBRtsyWBkn5EixH-vMaraxtPzd-d35zdDoxmHCiwh8bPEzmCfTHk9RP58vnxFSfIe3UgqtaEgA_TFZ3TVkxy6jW76-fkf-mHQio0G-WMKMfTc9CiZX2teG2ogwXteQ-Ul4y06RTXUw-Jb0ZG-PYYGKjKOx-BG9vuR__DCJGkDVYvKeqg0Mu6vM9BjXCPopCXv2Oihld3KnVEeC6LRVmm6lnedJOHuu0b3qZVMoCExncq0zMsj5gUvDwW-FQVr7tnp2OavWcsO-yxHWJYYeJh_3fIOsS_fJRN5Uw)
```mermaid
  stateDiagram-v2
    [*] --> Still
    Still --> [*]
    Still --> Moving
    Moving --> Still
    Moving --> Crash
    Crash --> [*]
```


##### 8. [ER Diagram](https://mermaid.live/edit#pako:eNp1klFvgjAUhf8Kuc8iEzdU3gyQxWSOBdDEhJdKL9AEqCnFxAD_fUUlmy7rW0-_nnNz720h4RTBBhQuI5kgZVxp6ji7MPK3XqD13XTatZrrfWz2XnDQ164beGGo2VpO6ie263Sdt5ofuOpia6eCJPgPs_nc-xvHU1QMBSPHArWUixhu9J-0J2eBCbLz6D16DVD3AyX8jOKO3LTfgL6JvK2iWJUUDR2tvgLf3TmR7qwj790PDuOXu351rSRh1SP_UN_oHAMXFAVSlREDTKBEURJGVbPb4XcMMscSYxhQiilpCjk0oFcoaSQPL1UCthQNTqA5USLxPqFH0aNMcgF2SopaiQUnKhTsFuTlNAw2Y7VUjqrulGWD3ohCybmUp9o2jOF5mjGZN8dpwkujZjQnQubnlWVYprUk5hytxZy8zec0Oc5Wy9R8naV08TIzCfT9BPCav71t0XWZ-m_B4LnJ)
```mermaid
  erDiagram
    CUSTOMER }|..|{ DELIVERY : has
    CUSTOMER ||--o{ Order : place
    CUSTOMER ||--o{ INVOICE : "liable for"
    DELIVERY ||--o{ Order : receives
    INVOICE ||--|{ Order : covers
    Order ||--|{ Order-ITEM : includes
    PRODUCT-CATEGORY ||--|{ PRODUCT : contains
    PRODUCT ||--o{ Order-ITEM : "ordered in"
```


##### 9. code

<pre>
<code>
    test....
    
</code>
</pre>
  



##### 10. 📖 Gantt :fire:

```mermaid
gantt
    title A Gantt Diagram
    dateFormat  YY-MM-DD
    section AI
    AI 기술테스트  : a1, 20-10-14, 10d
    가상 얼굴 학습 및 환경세팅  : 20-10-14, 10d
    얼굴 인식 개선 및 적용 : after a1, 10d
    가상 얼굴 이미지 생성 및 분류 : after a1, 4d

    section Front-end
    와이어프레임     :a1,20-10-14  , 10d
    react 학습 및 적용 : after a1,  10d
    사진 업로드 및 설정 기능 :after a1 , 10d

    section Back-end
    django 학습 및 적용 : a1,20-10-14 , 10d
    회원기능      :a2,after a1 , 10d
    친구기능      :after a1  ,10d
    결과 이미지저장,공유  : a3,after a2, 2d
    스티커 기능  : a4,after a3, 2d
```



### 1 칸 띄우기

[칸 띄우기](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbjKx6J%2FbtqIOarD9DF%2FxH33ypKG8Zyi7SGLQeT241%2Fimg.png)


### 2 형광색 처리

<span style='background-color: #fff5b1'>Yellow</span>  
<span style='background-color: #f6f8fa'>Gray</span>  
<span style='background-color: #f1f8ff'>Blue</span>  
<span style='background-color: #ffdce0'>Red</span>  
<span style='background-color: #dcffe4'>Green</span>  
<span style='background-color: #f0f0ff'>Pupple</span>  
<span style='background-color: #f7d0be'>Orange</span>  


### 3 코딩 블록 입히기

    ㅁ In: buf  
    ㅁ Format:  


### 수식
#### latex 적용
a. latex.codecogs.com 홈페이지 접속
b. 변환하고자 하는 수식 입력
c. 출력된 이미지를 우측 마우스 클릭 후 이미지 주소 복사
d. 복사된 이미지 url을 마크다운으로 임베딩

![](복사된 url)

예)
![](https://latex.codecogs.com/png.latex?%5Cfrac%7Bd_x%7D%20%7Bd_t%7D)

#### Tex 적용
![editRules_tex](https://user-images.githubusercontent.com/54181684/183279212-5b1cdae9-23e0-4a63-a466-5111739c1dcd.png)



[Ref.](https://www.math.brown.edu/johsilve/ReferenceCards/TeXRefCard.v1.5.pdf)


### 1 문단 (Paragraph)  

### 2 제목 (Header)  
  - 간편 설정 : === & ---  
  - 헤더 설정 : #  

### 3 블록 인용구  
  - '>' (블럭인용문자, Block quote)  
  - '>>', '>>>' 사용하면 여러 층 사용  

### 4 코드 (Code)  
코드 블럭 (Code Block) : ''' 혹은 \~\~~ 으로 감싼 텍스트  
혹은 줄의 맨 앞에 스페이스 4개가 삽입되었을 때.  
인라인 코드 (Inline Code) : \`로 감싼 텍스트  

- 코드블럭 예) Tab 삽입(스페이스 4개 삽입의 경우 되다 안되다 한다...)

```  
코드 예)
  code example 
```

- 코드블럭 예) 코드("```") 이용
```
public class BootSpringBootApplication {
  public static void main(String[] args) {
    System.out.println("Hello, Honeymon");
  }
}
```


### 7 목록 (List)
7.1 번호 목록 (Ordered List)
- 숫자와 점을 이용하여 목록 생성

7.2 기호 목록 (Unordered List)
-,+,\*을 사용해 기호 목록 생성, 계층별로 나누고 싶으면 tab을 삽입


### 8 링크 (Link)  
8.1 외부 링크 (External Link)  
인라인 링크 : [링크](http://example.com"링크 제목")  
[연습](http://www.naver.com)  

참조 링크 : [링크1][1] & [1]: http://example1.com/ "링크제목1"  
URL 링크 : <example.com/> & <example@example.com>  
8.2 내부 링크 (Internal Link)  


### 9 표 (Table)  
9.1 정렬 (Alignment)  
  - ':' 를 헤더의 양쪽 혹은 한쪽에 삽입
  -   
9.2 열 병합 (Column spanning)  
| Column 1 | Column 2 | Column 3 | Column 4 |  
| -------- | :------: | -------- | -------- |  
| No span  | Span across three columns    |||  

<table>
   <tbody>
      <tr>
         <td><b>followerId</b></td>
         <td><b>followingId</b></td>
      </tr>
      <tr>
         <td>text_1</td>
         <td>description of text_1</td>
      </tr>
      <tr>
         <td>text_2</td>
         <td>description of text_2</td>
      </tr>
      <tr>
         <td>text_3</td>
         <td>description of text_3</td>
      </tr>     
   </tbody>
</table>


### 10 이미지 (Image) 
: `![이미지 이름](이미지 주소)`  


### 11 이스케이프(Backslash Escape) 
: \\  
마크다운 작성 중 \*이나 \_ 을 사용하고 싶은 경우, 해당 기호 앞에 \\를 삽입  

### 14. 각주  
각주[^14]  

[^14]: 1234567890
