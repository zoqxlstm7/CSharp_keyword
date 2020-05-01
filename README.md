# C# 키워드 정리
## object
### 객체의 데이터 형태
- 어떤 데이터 형이든 모두 처리 가능
- 클래스에 상속이 적용 됨
> object와 관련된 레퍼런스만 사용 가능
## var
### 암시적 형식 지역 변수
- 선언과 동시에 반드시 초기화
- 지역 변수로만 사용 가능
- 'for~each'에서 자주 사용
> 초기화된 타입에 관련된 레퍼런스 사용 가능
## nullable
- 기존 데이터형의 값 + null값 저장이 가능
- 사용법 : 데이터 자료형? 식별자
- int? num = 100;
- HasValue, Value 사용
```c#
int? a = 10;
int? b = null;
bool? isFlag = null;

// 값이 있는지 확인 (true, false 반환)
Console.WriteLine(isFlag.HasValue);
// 값을 참조하려면 반드시  null이 아닌지 체크
if(isFlag.HasValue)
    Console.WriteLine(isFlag.Value);
```
## null 병합 연산자
### null값을 체크하는 연산자
> null인가 ?? 처리1
```c#
int? a = null;
int b = 10;
// a가 null이면 b값 대입
// null이 아니면 a값 대입
int result = a ?? b; // 10

int? c = null;
int = 100;
result = a ?? c ?? d // 100

c = 1000
result = a ?? c ?? d // 1000
```
## params
### 파라미터를 제한없이 처리
```c#
int Total(params int[] valuse);
```
* * *
## is
### 객체의 형식 검사
- bool 리턴
```c#
class AA {}
class BB {}

if(aa is BB)
else if(aa is AA)
```
* * *
## as 
### 형식 변환
- null 리턴
```c#
class BB {}

BB copyBB = bb as BB;
```
* * *
## sealed
### 상속과 재정의 불가
#### 클래스 sealed
```c#
sealed class CC {}
class DD : CC {} // 오류
```
#### 함수 sealed
```c#
class AAA
    public virtual void Print();
class BBB : AAA
    public sealed override void Print();

class CCC : BBB
    public override void Print(); // 오류
```
* * *
## 클래스 HAS-A관계
### 클래스가 다른 클래스를 가지는 구조
- 두 개의 클래스가 매우 강한 연관성을 가진다.
```c#
class AA {}
class BB
{
    AA[] aa; // HAS-A 관계
}
```
* * *
## partial 
### 클래스를 나누어서 구현
- 컨텐츠별로 구분해서 코딩 가능
```c#
partial class AA {}
```
> AA.ADD.cs  
> AA.cs  
> AA.MUL.cs
* * *
## 확장 메소드
### this 키워드
```c#
class AA
{
    public void View(string str) {}
}

static class Utill
{
    public static void Print(this AA aa, string str){
        aa.View(str);
    }

    public static void Sum(this int a){
        Console.WriteLine("{0} + {1} = {0}", a, a, a + a)
    }
}
```
```c#
static void Main()
{
    AA aa = new AA();

    Util.Print(aa, "Print"); // 기본적인 클래스 내 함수 호출
    aa.Print("Print"); // this 키워드를 통해 가능

    Util.Sum(10);
    10.Sum(); //this 키워드를 통해 가능
}
```
* * *
## 클래스 vs 구조체
### 클래스
- 참조타입 - 힙에 생성
- new 연산자
- 파라미터 없는 생성자 가능
### 구조체
- 값 타입 - 스택에 생성
- new 연산자 없는 생성 가능
- 생성자 호출 시 반드시 파라미터가 있어야 함
#### 구조체의 사용
- 자료의 크기가 작을 때
- 구조가 단순할 때
* * *
## 인터페이스
### 다중 상속
- 메소드, 이벤트, 인덱서, 프로퍼티 사용 가능
- 필드, 접근제한자 사용 불가
- 구현부(정의) 없음
- 인스턴스 생성 불가(참조 가능)
```c#
interface IAA
{
    //int a; // 오류
    //public void IPrint(); // 오류

    int A { get; set; }
    //강제적으로 상속받은 클래스에서 구현부를 정의
    void IAAPrint();
}
```
#### 참조 가능
```c#
class AA : IAA {}
class BB : IBB {}

BB bb = new BB();

// 참조
IAA iaa = new AA();
IBB ibb = bb as IBB;
```
* * *
## 추상 클래스
### 상속 받는 클래스의 규격 지정
- 인스턴스 생성 불가(참조 가능)
- 구현부 없음
```c#
abstract class abstractAA
{
    private int a;

    public abstractAA() {}

    //강제적으로 상속받은 클래스에서 구현부를 정의
    public abstract void APrint(); 
    public virtual void VPrint(); // 가상 함수
    public void Print(); // 일반 함수
}
```
* * *
## 프로퍼티
### 정보 은닉
- get, set 키워드
- set부분을 구현하지 않으면 readonly와 같은 읽기 전용
```c#
private int num;

public int NUM
{
    get { return num; }
    set { num = value; }
}

public int NUM { get; set; }
public int num2 { get; private set; }
public string NAME { get; set; } = "Name";
```
* * *
## 컬렉션 (Collection)
### 자료구조
- 데이터 저장, 검색, 기타 데이터 처리 특화
> Using System.Collections;
#### ArrayList
> Add()
#### Stack
> push()  
> pop()  
> peek()
#### Queue
> Enqueue()  
> Dequeue()  
> peek()
#### Hashtable
- 키와 값이 쌍으로 구성되는 데이터
- 탐색 속도가 빠르고 사용이 편리
##### 선언 및 초기화
```c#
Hashtable hashTable = new Hashtable();
hashTable.Add("name", "jack");
hashTable["weight"] = 10.8f;
```
```c#
Hashtable hashTable = new Hashtable()
{
    ["pos"] = 10,
    ["name"] = "jack",
    ["weight"] = 10.8f,
};
```
##### 사용
```c#
foreach(object key in hashTable.keys)
    Console.WriteLine("data: {0}", hashTable[key]);
```
* * *
#### 인덱서
- 배열 or 컬렉션의 외부 접근
- 키워드 : get, set, return, value, this[int index]
##### 선언
```c#
class AA
{
    private int[] num = new int[10];

    public int this[int index]
    {
        get { return num[index]; }
        set { num[index] = value; }
    }
}
```
##### 사용
```c#
AA aa = new AA();

aa[0] = 1;
aa[1] = 2;
... 
```
* * *
## 일반화 프로그래밍
### 클래스 및 함수 일반화
- Boxing, UnBoxing을 줄일 수 있음
- 불필요한 오버로딩을 줄일 수 있음
#### 함수 일반화
```c#
public void Print<T>(T data) { }
public void Print<T>(T[] arrData) { }
```
#### 클래스 일반화
```c#
class AA<T>
{
    private T num;
    
    public T GetNum(){
        return num;
    }

    public void SetNum(T data){
        num = data;
    }
}
```
```c#
AA<int> AA = new AA<int>();
AA<float> BB = new AA<float>();
```
#### dynamic
- 런타임 시 변수 형식 결정
- 일반화 함수에서 변수타입 대응 가능
- 매개변수로 사용 가능
- Boxing, UnBoxing이 없다
```c#
static T AddArray<T>(T[] arrDatas){
    dynamic temp = 0;
}
```
#### default
- value type: 0으로 초기화
- reference type: null로 초기화
```c#
T temp = default(T);
for(int i = 0; i <arrDatas.Length; ++i){
    temp += (dynamic)arrDatas[i];
}
```
#### where (한정자)
- 매개변수 제한 기능
```c#
class AA<T> where T : struct {} // 값 형식으로 제한
class BB<T> where T : class {}  // 참조 형식으로 제한
```
```c#
interface II {}
class CC<T> where T : II {}    // interface로 제한
```
#### 일반화 컬렉션 (Collections Generic)
- 컬렉션의 박싱과 언박싱의 단점을 해결
> using System.Collections.Generic;
##### List< T >
##### Queue< T >
##### Stack< T >
##### Dictionary< T >
- 키와 값으로 구성
###### 선언 및 초기화
```c#
Dictionary<string, int> dic = new Dictionary<string, int>();
dic.Add("10", 10);
dic["20"] = 20;

Dictionary<int, string> dic = new Dictionary<int, string>() {
    [1] = "H",
    [100] = "O",
    [1000] = "Good",
}
```
###### 사용
```c#
foreach(var key in dic.Keys)
    Console.WriteLine(dic[key]);
```
```c#
string getValue = string.Empty;
// key값이 트루 일때 값을 얻어옴
// false일 때 null값 반환
dic.TryGetValue(1, out getValue);
```
* * *
## 예외 처리
### 프로그램의 안정성과 가독성을 높일 수 있다.
#### 사용자 정의 예외 처리
- 기존 예외 처리 클래스에서 상속
- Exception Class를 바로 상속받는 것은 지양
- ApplicationException Class를 일반적으로 상속받아 사용
```c#
class MyException : ApplicationException
{
    public int Num { get; set; }
    
    public MyException():base(){
    }
    
    public MyException(int a){
        Num  = a;
    }

    public override string ToString(){
        return "Num: " + Num;
    }
}
```
#### when
- throw된 예외 비교 처리
```c#
catch(MyException e) when(e.Num == 0) 
{ 
    // 실행 코드
}
```
#### StackTrace
- 예외가 발생했을 때의 마지막으로 호출된 위치 출력
```c#
catch(MyException e)
{ 
    Console.WriteLine("MyException: " + e.StackTrace);
}
```
* * *
## 델리게이트
### CallBack 함수
#### 선언 방법
```c#
void Sum(int a, int b) { ... }
delegate void DelegateTest(int a, int b);
```
- 기본 선언
```c#
DelegateTest dt = new DelegateTest(Sum);
```
- 간략한 선언
```c#
DelegateTest dt = Sum;
```
- 익명 함수 선언
```c#
DelegateTest dt = delegate(int a, int b)
{
    // 실행 코드
};
```
- 람다식 선언
```c#
DelegateTest dt = (a, b) => {
    // 실행 코드
};
```
### 델레게이트 함수 파라미터 활용
- 함수의 확장성을 높일 수 있다.
```c#
delegate void DelegateFunc();

DelegateFunc CallOkFunc;  
DelegateFunc CallCancelFunc;
```
```c#
public void Message(string msg, DelegateFunc OkFunc, DelegateFunc CancelFunc)
{
    CallOkFunc = okFunc;
    CallCancelFunc = CancelFunc;
}
```
* * *
## 이벤트(event)
### 정보은닉, 캡슐화 목적 
- 클래스 내부 상태변화, 이벤트 발생 처리에 사용
- 클래스 외부 사용 시 클래스 내부 이벤트 호출 함수 필요
- delegate와 차이점
    - 할당 연산자(=) 사용 불가
    - 클래스 외부 호출 불가
    - 클래스 멤버 필드에서 사용
```c#
public delegate void delegateEvent(string msg);
public event delegateEvent myEvent;
```
* * *
## 람다식
### 익명 메소드
- 메소드와 동일하게 입력(파라미터), 출력(리턴) 존재
- (매개변수) => { 함수내부(식); };
```c#
(str) => { Console.WriteLine(str); }; // 람다 함수
delegateA = (a) => { return a + a; }; // 델리게이트 람다 함수
```
### 리스트와 람다식 - 참고
- 리스트 함수 중 delegate파라미터
- Collections에서 다양하게 활용
```c#
listData.FindAll( (num) => { return num < 200; } );
listData.Find( (num) = > num % 2 == 0) );
```
```c#
static void Main()
{
    List<int> listData = new List<int> { 1, 2, 3, 100, 200, 300 };

    // public delegate bool Predicate<in T>(T obj);
    // public List<T> FindAll(Predicate<T> match);
    List<int> listFindAll = listData.FindAll( (num) => { return num < 200; });

    // 200보다 작은 수 => listFindAll

    int findNum = listData.Find( (num) => num % 2 == 0 );

    // 첫번째 짝수 => findNum
}
```
### 함수와 람다식
#### 람다식 파라미터 사용법
```c#
delegate void dPrint(string str);
static public void CallBackFunc(dPrint dp, string msg);
```
- 함수 연결
```c#
CallBackFunc(CallPrint, "Hello");
```
- 델리게이트 직접 전달
```c#
CallBackFunc(delegate(string str) { Console.WriteLine(str); }, "Hello");
```
- 람다의 식형태
```c#
CallBackFunc((string str) => { Console.WriteLine(str); }, "Hello");
```
- 람다식 기본
```c#
CallBackFunc((str) => Console.WriteLine(str), "Hello");
CallBackFunc(str => Console.WriteLine(str), "Hello");
```
- 파라미터가 없는 람다식
```c#
() => Console.WriteLine("No Params");
```
* * *
## Action
### 미리 선언된 리턴값이 "없는" 델리게이트 일반화 함수
#### public delegate void Action();

#### public delegate void Action<in T1, in T2, in T3>(T1 arg1, T2 arg2, T3 arg3);
```c#
static void Main()
{
    Action aFunc;
    Action<int> aFunc2;
    Action<float, int> aFunc3;

    aFunc = CallAction;
    aFunc2 = (num) => Console.WriteLine("num: " + num);
    afunc3 = (a, b) => {
        float result = b / a;
        Console.WriteLine("a: " + a + " b: " + b + " result: " + result);
    }

    aFunc();
    aFunc2(100);
    aFunc3(6.0f, 10);
}
```
* * *
## Func
### 미리 선언된 리턴값이 "있는" 델리게이트 일반화 함수
- 반환형은 항상 마지막으로
#### public delegate TResult Func<out TResult>();
#### public delegate TResult Func<in T1, in T2, in T3, out TResult>(T1 arg1, T2 arg2 , T3 arg3);
```c#
static void Main()
{
    Func<int> aFunc; // 매개변수 없음
    Func<int, float> aFunc2; // 매개변수 int, 반환형 float
    Func<int, int, int> aFunc3; // 매개변수 int, int 반환형 int

    aFunc = CallFunc;
    aFunc = (int a) => { return (float)(a / 2.0f); };
    aFunc3 = (a, b) => (a + b);

    Console.WriteLine("aFunc: " + aFunc());
    Console.WriteLine("aFunc2: " + aFunc2(10));
    Console.WriteLine("aFunc3: " + aFunc3(100, 100));
}
```
* * *
## LINQ (Language-Integrated Query)
### 쿼리 기능 지원
#### from: 어디에서 찾을 것인지
> from 범위 변수 in 데이터 원본
#### where: 조건이 무엇인지
> where 조건식
#### select: 어떤 것을 가져올 것인지
> select 범위 변수
```c#
var QueryData = // IEnumerable<int>
    from temp int data
    where temp < 100
    select temp;
```
- LINQ 기초 예제
```c#
static void Main()
{
    int[] data = new int[] { 0, 54, 98, 102, 332 };

    var QueryData = // IEnumerable<int>
        from temp int data
        where temp < 100
        select temp;

    var test = from temp int data
               select temp;
    
    foreach(int n in QueryData){
        Console.WriteLine("QueryData: " + n);
    }

    // 람다식 사용과 비교
    List<int> listData = new List<int>(data);
    List<int> findAllData = listData.FindAll(a => a < 100);

    foreach(int n in findAllData){
        Console.WriteLine("findAllData: " + n);
    }
}
```
### select
- 결과를 선택
- LINQ쿼리식 끝나는 부분
- 특정 형식으로 변환 가능
```c#
var QueryData =
    from data int arrStudents
    where data._id > 200 && data._kor > 50
    // 새로운 형싱으로 변환
    select new {
        id = data._id,
        name = data._name,
        total = data._kor + data._eng
    };
```
### orderby
- 데이터 정렬
- ascending 키워드 (오름차순)
- descending 키워드 (내림차순)
- "," 콤마로 둘 이상의 데이터 정렬
```c#
var QueryData = 
    from data in arrStudents
    orderby (data._kor + data._eng) descending // 내림차순 정렬
    //orderby (data._kor + data._eng) ascending // 오름차순 정렬
    select data;
```
### group
- 데이터 분류 후 그룹화
- group 범위 by 분류기준 into 그룹변수
```c#
var QueryData = 
    from data in arrStudents
    orderby (data._eng + data._kor) descending
    group data by (data._eng + data._kor) < 150;
```
- 사용 예제
```c#
static void Main()
{
    var QueryData = 
    from data in arrStudents
    orderby (data._eng + data._kor) descending
    // 비교 연산자를 사용했기 때문에 data의 key값은 true 또는 false가 된다.
    group data by (data._eng + data._kor) < 150;

    // QueryData에는 두개의 data가 들어있다.
    foreach(var data in QueryData){
        string str = data.key ? "합이 150보다 작은경우: " : "합이 150보다 큰경우: ";
        Console.WriteLine(str);

        foreach(var item in data){
            Console.WriteLine("\t{0}: {1}", item._name, (item._kor + item._eng));
        }
    }

    // 다른 방식으로 분리해서 비교하기
    List<Student> listMaxStudents = null;
    List<Student> listMinStudents = null;

    foreach(var data in QueryData){
        if(false == data.key)   // 합이 150보다 큰경우
            listMaxStudents = data.ToList();
        else
            listMinStudents = data.ToList();
    }

    // 분리된 두 리스트를 원하는대로 처리
    // ex) 재그룹화, 재정렬 등
    // 여기서는 단순 출력 실행
    for(int i = 0; i < listMaxStudents.Count; ++i){
        Console.WriteLine("합이 150보다 큰경우: " + listMaxStudents[i]._name);
    }

    for(int i = 0; i < listMinStudents.Count; ++i){
        Console.WriteLine("합이 150보다 작은경우: " + listMinStudents[i]._name);
    }
}
```
### gourp의 활용 - into
- 그룹화하여 그룹변수에 저장
```c#
static void Main()
{
    var QueryData = 
        from data in arrStudents
        // 평균을 열 구간으로 나눔 0~9
        group data by ((data._eng + data._kor) / 2) / 10 into gTemp
        orderby gTemp.key ascending
        select gTemp;

    foreach(var data in QueryData){
        Console.WriteLine("data: {0}에서 {1}", data.key * 10, (data.key + 1) * 10);

        foreach(var item in data){
            Console.WriteLine("\t name: {0}, avg: {1}", item._name, (item._kor + item._eng) / 2f);
        }
    }
}
```
### join
- 두개의 데이터를 연결
#### 내부 조인
```c#
var QueryData = 
    from data in arrStudents
    join detail in arrDetails on data._name equals detail._name
    select new {
        name = data._name,
        total = data._eng + data._kor,
        gender = (detail.gender == 0) ? "여자" : "남자"
    };
```
#### 외부 조인
```c#
var QueryData = 
    from data in arrStudents
    join detail in arrDetails on data._name equals detail._name into inData
    // 데이터가 비어있다면 생성해 준다
    from detail in inData.DefaultIfEmpty(new Detail() { gender = 1 })
    select new {
        name = data._name,
        total = data._eng + data._kor,
        gender = (detail.gender == 0) ? "여자" : "남자"
    };
```
## 파일 처리
> using System.IO;
### 스트림 (Stream)
- 파일, 네트워크 등에서 사용
- File & Directory 클래스
#### 파일 생성
```c#
// 경로를 이용해 파일 생성
FileStream fs = File.Create(path);
// 파일이 존재하는지 확인
File.Exists(path);
// 파일이 생성된 시간 반환
File.GetCreationTime(path);
```
```c#
// FileInfo 클래스를 이용한 파일 생성
FileInfo fileInfo = new FileInfo("b.txt");
FileStream fs = fileInfo.Create();

// 메모리 반환
fs.close();
// 파일 복사
File.Copy("a.txt", "c.txt");
// 파일 복사
FileInfo dst = fileInfo.CopyTo("d.txt");
```
### 바이트 입출력
- FileStream, BitConverter
- 데이터 형식을 byte 배열로 변환(BitConverter)
#### 쓰기
```c#
long lValue = 123456789123456789;
Stream outStream = new FileStream(fileName, FileMode.Create);
byte[] wBytes = BitConverter.GetBytes(lValue);
outStream.Write(wBytes, 0, wBytes.Length);
```
#### 읽기
```c#
FileStream inStream = new FileStream(fileName, FileMode.Open);
byte[] rBytes = new byte[sizeof(long)];
inStream.Read(rBytes, 0, rBytes.Length);
long readValue = BitConverter.ToInt64(rBytes, 0);
```
### 텍스트 입출력
- StreamWriter, StreamReader
#### 쓰기
```c#
FileStream fsWrite = new FileStream("a.txt", FileMode.Create);
StreamWrite sw = new StreamWriter(fsWrite);

sw.Write("Hello World");

sw.Close();
```
#### 읽기
```c#
FileStream fsRead = File.Open("a.txt", FileMode.Open);
StreamReader sr = new StreamReader(fsRead);

while(false == sr.EndofStream){
    Console.WriteLine(sr.ReadLine());
}

sr.Close();
```
#### 단독 사용 가능
```c#
StreamWriter sw = new StreamWriter("b.txt");

sw.WriteLine("Hello World");

sw.Close();
```
```c#
StreamReader sr = new StreamReader("b.txt");

while(false == sr.EndOfStream){
    Console.WriteLine(sr.ReadLine());
}

sr.Close();
```
### 사용자 정의 입출력
- [Serializable]
- BinaryFormatter, Serialize, Deserialize
> using System.Runtime.Serialization.Formatters.Binary;
```c#
[Serializable]
struct Player
{
    public string Name { get; set; }
    public int Level { get; set; }
    public double Exp { get; set; }
}
```
#### 쓰기
```c#
FileStream fsW = new FileStream("savePlayer.txt", FileMode.Create);
BinaryFormatter bf = new BinaryFormatter();
bf.Serialize(fsW, player);
fsW.Close();
```
#### 읽기
```c#
FileStream fsR = new FileStream("savePlayer.txt", FileMode.Openn);
BinaryFormatter bf = new BinaryFormatter();
Player[] readPlayer = (Player[])bf.Deserialize(fsR);
fsR.Close();
```
### 이진 입출력
- BinaryWriter, BinaryReader
- 모든 기본 데이터 형식에 읽고 쓰기 오버로딩
#### 쓰기
```c#
FileStream fs = new FileStream(fileName, FileMode.Create);
BinaryWriter bw = new BinaryWriter(fs);

bw.Write(100);
bw.Write(100.001f);
```
#### 읽기
```c#
FileStream fs = new FileStream(fileName, FileMode.Open);
BinaryReader br = new BinaryReader(fs);

int num = br.ReadInt32();
float fNum == br.ReadSingle();
```
### CSV 데이터 활용
- 게임 데이터 협업
- String.Split 활용
```c#
string str = "0, 1, 2, 3, 4, 5";
string[] splitRead = str.Split(',');

for(int i = 0; i < splitRead.Length; ++i){
    Console.Write(" {0} ", splitRead[i]);
}
```