# 0. 주석 
- 설명역할, 코드로 인식되지 않음. (//으로 시작)
- 단축키 블록 지정 후 control+k+c(주석으로 변환) / control+k+u (주석지정 해제)

---
	
# 1. 자료형 
- 변수의 자료 형태를 설명하는 역할 (크기단위, Byte)
  그 자체로는 어떠한 실체도 없음. Data Type


### 1.1 종류 
- 정수형 : char(1Byte), short(2Byte), int(4Byte), long(4Byte), long long(8Byte) 등
- 실수형 : float(4Byte), double(8Byte) 등
- 정수형과 실수형을 구분하는 이유 : 정수타입 데이터와 실수타입 데이터를 처리하는 방식 자체가 완전히 다름.

ex) int i = 0;
>int : 자료형(고유형태로,이름 임의로 변경불가)
	i : 변수명(임의대로 변경 가능)
	i라는 변수의 데이터 크기는 4Byte, 정수타입의 데이터가 저장되고 그 공간의 이름을 i라고 설정함. 그리고 초기값으로 0을 넣음.

### 1.2 Byte?
- 1byte = 8bit
- bit = 더이상 쪼갤 수 없는 최소 단위, 0또는 1만 표현 가능
- 2^10 = 1024 Byte = 1KB
- 1024 KB = 1MB
- 1024 MB = 1GB
- 1024 GB = 1TB = 2^40 Byte
- 8bit 의 표현 가짓수 = 2^8 = 256 가지 (표현 가능한 양수 정수의 범위 = 0~255)

------------

# 1-1 정수형 자료형 
:char(1Byte), short(2Byte), int(4Byte), long(4Byte), long long(8Byte) 등

```
unsigned char c = 0;
```
> 양(unsigned)의 정수형의 1byte 자료 
> c는 1바이트로 양수만 표현 = 0~255의 양의 정수값을 가질 수 있음
c = 0; (c에 0의 값을 넣어줘/등호X,대입)
c = 256; (11111111(255)+1==100000000이지만, 자료형에의해 결과값 00000000(0))
c = -1; 

```
char c1 = 0;
signed char c1 = 0; 
```
> 위 아래 같은 문장으로, 위 문장은 signed 가 생략된것
> c1은 1바이트로 양수, 음수 둘 다 표현 = -128~0~127 정수값을 가질 수 있음 (음수 128개, 양수 128개 총 256개)
> 8bit 의 첫자리가 0일때 양수, 1일때 음수 (첫자리 제외한 나머지 7칸으로 2^7=128가지 표현)
첫자리 = MSB (Most Significunt Bit 가장 중요한 Bit)
음수(-x)의 bit 표현 : 특정 양수(X) 를 bit로 표현하여 x+(-x)=0 이 되는 경우
01111111 -> 127
10000001 -> -127
00000001 -> 1
11111111 -> -1
10000000 -> -128

* c1 = 255; 
결과값은 -1
> c = 255 와 c1 = -1의 bit 표현은 같음!
> 동일한 bit 공간에 동일한 값이 들어가 있어도 그걸 읽어내는 자료형에 따라 결과값이 달라 질 수 있음! 

* 음수표현 쉽게 계산하는 법 = 2의 보수법 = 원래 양수 비트를 반전시킨 후 +1 시킴
음수의 개념 = 대응하는 양수와 더했을 때 0이되는 숫자

>ex)
1. 0000 0010 -> 2
  0과 1 반전
2. 1111 1101
1 더하기
3. 1111 1110 -> -2


* 1Byte = 2^8 = 256
2Byte = 2^16 = 65,536
4Byte = 2^32 = 42억
	  
# 1-2. 실수형 자료형 
:float(4Byte), double(8Byte) 등

실수라는것은 0~1사이만 해도 무한대, 어떻게 한정적 bit 안에서 표현 할 수 있을까?
- 정수와 실수는 표현방식 자체가 다름, 정수처럼 1:1 매칭이 아닌 가장 근사값을 표현함.
정수와 실수가 연산에서 혼합되어있을때에 둘중 하나의방식으로 바꿔야함.

ex) int a = 4 + 4.0; = 8 
> 여기서 눈에 보이진 않지만 4.0이라는 실수를 4라는 정수체계로 바꾸는 형변환이라는 연산이 들어감.
> 충분한 의도가 아니면 가급적 정수는 정수끼리, 실수는 실수끼리 계산
> 정수와 실수 두 표현방식의 피 연산자가 연산될 경우, 명시적으로 반환

ex) float f = 10.2415f + (float)20;
>(float)생략해도 연산은 가능하나, 명시적으로 명확하게 작성
> 10.2415 뒤 f 는 double 이 아닌 float 으로 계산하겠다는 표현

* float 보다 double이 훨씬 더 낮은 단위의 소수점까지 표현, 정밀도가 높음.
* 부동소수점 
>ex)
21.8125
21을 변환 > 10101
10101 뒤 1은 0.5(2^(-1)=1/2=0.5)의미 그 뒤 1은 2^(-2)(=0.25)
0.8125  > 0.1101
21.8125 > 10101.1101
위를 정규화(소수점을 맨 앞으로 땡김)하면
0.101011101*2^5
지수 5를 이진법으로 바꾸면 101
0 00000101 10101110100000000000000
> 부호(1) 지수(8) 가수(23)

# 2. 연산자


## 2-1. 대입연산자 

ex) int i = 0
>여기서 (=)은 0을 i에 값을 넣는 대입 연산자.

## 2-2. 산술 연산자
##### :   +, -, &#42;, /, %(모듈러스 연산자, 나머지 연산자)

ex) int data = 10 + 10;
> 산술연산자 먼저 수행후 대입연산자 후순위로 수행.
data + 20;
> 실행하면 data에 20을 더하긴하지만 그 결과를 넣을 곳을 지정하지 않았기때문에 별도로 저장하지 않음.
data = data + 20;
data += 20;
> 위 아래 같은 문장.
> += : 뒤의 값을 더해서 변수에 대입까지 하는 연산자.
> 둘다 실행하면 결과값 40 산출


#####  나누기 연산(/)과 나머지 연산

	ex) data = 10/3;
> 실행값은 3

	data = 10%3;
> 실행값은 1

피연산자가 정수인지 실수인지에 따라 2가지 케이스 발생.

실수끼리는 나머지가 발생하지 않기때문에 나머지 연산시 오류 발생.	
둘중 하나가 실수여도 나머지 연산시 오류 발생.
따라서 둘 다 정수일 경우에만 나머지 연산 가능.


#####  실수끼리 나누기 
ex) data = 10. / 3.;
> 실제 결과값은 실수이나, data 를 받는 자료형이 정수형이기때문에 결과는 정수(3)으로 나옴.
> 실행은 가능하나 경고 발생, double 을 int 로 변환하면서 소수점이하 상실
data = (int)(10./3.);
> 위와같이 바꿔 진행하면 경고 사라짐.

## 2-3. 증감 연산자
##### :  ++, - -

data = 0;
data ++;

> 실행값은 1

data ++;
> 실행값은 2

data = 0;
data - -;
> 실행값은 -1


data - -;
> 실행값은 -2


> 기본적으로 정수형의 계산에서는 (++)1이 증가하고, (- -)1이 감소한다.
> But, key 연산자에 따라 한단계가 증가 또는 감소한다고 표현 하는것이 더 맞음.
> 증감연산자는 대입(=)의 필요가 없이 실제 변수가 저장되어있는 값이 증가하거나 감소한 값으로 바뀐다.

ex) data = 0;
##### ++data; // 전위(전치)
##### data++;	// 후위(후치)
>  연산자 우선순위가 바뀜.
> 연산자가 뒤에 붙었을경우, 모든 연산자보다 후순위.(대입연산자보다도 후순위)

a = 10;
data = a++;
> 위를 실행했을 경우, a를 data에 넣고 난 후 증가, 따라서 data의 값은 10

a = 10;
data = ++a;
> 위를 실행했을 경우, a를 증가시킨 후에 data에 대입, 따라서 data의 값은 11

* 연산자는 가능한 습관적으로 전위로 사용할 것!


## 2-4. 논리 연산자 

* if /eslse 구문, switch case 구문(if/ eslse 구문과 유사)과 주로 같이 쓰임 

* 참(true), 거짓(false)

> 참 : 0이 아닌 값, 주로 1
> 거짓 : 0

ex)
int truefalse = true;
> 실행값은 1

int truefalse = false;
> 실행값은 0

ex)
bool truefalse = true;
> bool : 참 거짓 전용 자료형, 0과 1만 취급(굳이 따지자면 정수형),1Byte
bool IsTrue = 100;
> 100은 0이 아니기때문에 실행값은 1(true)


####  * !(NOT,반전, 역, 거짓을 참으로, 참을 거짓으로)

ex) IsTrue = true;
IsTrue = !IsTrue;
> 실행값은 0, 거짓(false)

ex) int iTrue = 100;
iTrue = !iTrue;
>100은 0이아니기때문에 참(true), 따라서 실행값은 그 반대인 0, 거짓(false)
int iTrue = 0;
iTrue = !iTrue;
>0은 거짓(false), 따라서 실행값은 그 반대인 1, 참(true)

#### * &&(AND,곱, 둘중 하나라도 거짓이면 거짓)
ex) iTrue = 100 && 200
> 둘다 참(0이 아님, true), 따라서 결과는 1(참)
iTrue = 0 && 200
> 둘중 하나가 0(거짓)이기 때문에, 결과는 0(거짓)

#### * ||(OR,합, 둘중 하나라도 참이면 참, 둘다 거짓이어야만 거짓)

ex) iTrue = 0 || 200 
> 둘중 하나가 참(0이 아님, true)이기 때문에, 결과는 1(참)
iTrue = 0 || 0
> 둘다 거짓(0, false)이기 때문에, 결과는 0(거짓)

## 2-5. 삼항 연산자
* ?:
* 논리연산자와 연계되어 같이 쓰임.
* 세개의 항이 있는 연산자 
> 문법 : 조건 ? true일때 : false일때 

ex) int a = 5;
int b = a<10 ? a : 10;
> a가 10보다 작을경우(조건), b에 a를 대입(참), 아닐경우 10을 대입(거짓)

* 가독성이 떨어질 수 있어서 선호하진 않음

## 2-6. 비교연산자

- == : 양쪽이 같니?
- |= : 양쪽이 다르니?
- < : 오른쪽이 더 크니?
- &gt; : 왼쪽이 더 크니?
- &lt;= : 오른쪽이 더 크거나 같니
- &gt;= : 왼쪽이 더 크거나 같니?


- 연산의 결과는 참 또는 거짓 


## 2-7. 비트 연산자

* 비트단위로 연산이 진행될 때 사용되는 연산자

-  비트 연산이라 함은, 실제 비트끼리 연산함을 의미. 비트단위로 연산을 진행.
- 비트 곱(&) : 둘다 1이여야 1, 둘중하나라도 0이면 0
- 합(|) : 둘중 하나만 1이여도 1, 둘 다 0이여야 0
- xor(^) : 두 자리가 같으면 0, 다르면 1
- 반전,not(~) : 0과 1을 반전, 0은 1로, 1은 0으로.

ex)
```
#define HUNGRY  1
#define THRISTY 2
#define TIRED   4 
#define FIRE    8
#define COLD    16
```
> TIRED 자리는 세번째 비트에 넣어야하기때문에 2^2=4
unsigned int iStatus = 0;

iStatus |= HUNGRY;  0000 0001
iStatus |= THIRSTY; 0000 0011

ex)	 상태값 체크
```
if (iStatus & THIRSTY)
{

}
```
> 곱이기때문에 둘다 1이여만 1이 나옴.
> iStatus 0000 0011
> THIRSTY 0000 0010
> 곱 하면 	  0000 0010 = THIRSTY

* 특정자리 비트 제거
ex) iStatus &= ~ THIRSTY;
> iStatus 예시 = 1110 1010 
> THIRSTY = 0000 0010
> ~THIRSTY = 1111 1101
> iStatus & ~THIRSTY 
1110 1010
1111 1101
결과 1110 1000
	
ex) 16진수 바꾸기!

10진수
```
#define HUNGRY  1
#define THRISTY 2
#define TIRED   4 
#define FIRE    8
#define COLD    16
```
16진수로 바꾸기
```
#define HUNGRY  0*1
#define THRISTY 0*2
#define TIRED   0*4
#define FIRE    0*8

#define COLD    0*10
#define POISON  0*20
#define POISON  0*40
#define POISON  0*80

#define POISON  0*100
#define POISON  0*200
#define POISON  0*400
#define POISON  0*800
```

## 2-8. 쉬프트연산자
#### <<,>> 방향대로 n칸을 밀어냄
ex)
```
unsigned char byte = 1;
byte <<= 1;
```
> 0000 0001 비트를 왼쪽으로 한칸 밀어넣으면 0000 0010, 10진법으로 2가 됨
> 통상 자리 한칸 이동 시, 10진법의 경우 10배, 2진법의 경우 2배
> (<<=) 는 이동 후 대입까지 실행, byte = byte<< 1; 과 같은 문장.

	byte <<= 3;
> 이 경우 3칸 왼쪽으로 이동, 8배 증가
> 2^n배수

	byte >>=1;
> 이 경우 1칸 오른쪽으로 이동
> 2^n 나눈 몫
> 나머지가 생기는 경우 밀려서 소실.

ex) 
```
0000 0011 (3)
>>1 적용
0000 0001 (1)
```
>끝의 1은 밀려서 소실 결과값은 1
결국 오른쪽으로 1칸 미는 것의 결과는 2로 나눈 몫

# 3. if/else 구문

ex) 
```
data = 0;
if (0&&200)
{
data = 100;
}
```
> ()안이 참이라면 {}실행
> (0&&200)은 거짓이기때문에 data = 0

ex)  if/else
```
if (data == 100)
{
//if 가 참인경우 수행
}
```
> data 는 100이 아니기때문에 {}안의 내용 실행되지 않음

```
else
{
//if가 거짓인경우 수행
}
```

ex) if /elseif/else
```
if()
{
if 가 참인경우 수행
}
else if()
{
if가 거짓인경우, 해당 else if 가 참인 경우 수행
}
else if()
{
if 와 첫번째 else if 가 모두 거짓일 경우, 해당 else if가 참인경우 수행
}
else
{
위 조건이 모두 거짓일때 수행
}
```
> else if 갯수는 무한대로 적용 가능 
> 마지막 else 는 없어도 가능함. else 가 없을 경우 모든 조건이 거짓일 경우 아무런 실행이 일어나지 않음.
> but 첫 if 의 조건만 검사되고 나머지(else if)는 조건이 검사되지 않음.




# 4. switch 구문

ex) if/else 구문과 비교
```
switch(10)					  int iTest = 10;
{									 if (iTest == 10)
	case 10:					 {
		break;					}
	case 20:					 else if(iTest ==20)
		break;					{
									  }
	default:					 else
		break;					{
}									 }
```
> switch(상수, 또는 변수)
> 밑에 case와 일치하는 부분 실행
> case 중에 일치하는 값 없으면 default 실행
> 왼쪽과 오른쪽은 동일한 의미.
> if else 구문이 더 다양한 조건 설정 가능하지만 조건이 복잡해질수록 가독성이 떨어짐.
> 반면 switch case 의 경우, case별로 정리하기때문에 가독성이 조금 더 좋음.

ex)
```
int iTest = 10;
switch (iTest)
{
	case 10:
	case 20:
	case 30:

		break;

	default:
		break;
}
```
> break 생략 시, break 걸린곳 까지 작동
> 위와 같이 의도적으로 생략하기도 함.
```
if(iTset == 10 || iTest = 20 || iTest ==30)
{
}
else
{
}
```
> 위 switch 구문과 동일.

# 5. 전처리기

- 컴파일 과정에서 무엇보다 우선하여 수행
- "#"으로 시작

- define
> 내가 지정한 구문을 특정 숫자로 치환해줌.
> 장점 : 가독성, 유지보수
ex) 
```
# define HUNGRY 1
```
> HUNGRY 를 1로 치환해줌(우선하여 치환)
```
int iStatus = HUNGRY
```
> int iStatus = 1 로 변환 된 후 컴파일 시작

-  숫자가 바뀔때 코드 전반적으로 돌아다니면서 수정할 필요가 없음. 유지보수측면에서 유리.


# 6. 변수

-  지역변수
: 괄호 안에 선언되어있는 변수

-  전역변수
: 괄호 외부에 선언되어있는 변수
- 정적변수
- 외부변수

- 지역과 전역을 나누는 기준 : 함수

- 변수 명 규칙 : 중복되는 이름 피하기. 

- 만약 지역 외와 지역 안 변수명이 중복될 경우 같은 영역(지역)이 우선순위로 같은 취급.

	
# 7. 함수(Funtion, 기능)

ex) data = 10 + 20; 를 함수로 만들기 
```
int Add(int left, int right)
{
int left + right;
}
data = Add(10,20);
```
* 함수 안에 또다른 함수를 만들 수 있음


