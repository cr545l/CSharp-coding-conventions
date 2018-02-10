# C# 코딩 컨벤션
### 개인적으로 정의한 코딩 컨벤션으로 공식 컨벤션이 아닙니다.

모든 규칙은 기본적으로 일관된 가독성 향상을 지향하기 위함으로 정의하였습니다.<br>

> ## 표기법
>
> 들여쓰기는 공백 4개<br>
> ( ) 의 내부는 항상 공백 추가<br>
> 주석은 한칸 띄우고(공백) 내용 입력<br>
>
>> ## 클래스, 함수, 프로퍼티, 델리게이트 `[파스칼 표기법]`<br>
>> 함수나 클래스 정의 간에 빈 줄 추가<br>
>>
>> ```
>> public class Class : IClass
>> {
>> 	public delegete void Delegate( int foo, bool bar );
>>
>>	public int Age { { get { return true; } } }
>>
>>	private void Function( int index )
>>	{
>>		for( int i = 0; i < count; i++ )
>>		{
>>			// ~
>>		}
>>	}
>> }
>> ```
>> ### 예외
>>
>> 변수, 함수, 프로퍼티의 헝가리안 표기는 is와 b에 한정하여 사용 (is는 프로퍼티 및 함수, b는 변수)<br>
>> [외부 접근 시 bool 결과를 분명하게 알 수 있고 편리하게 추론이 가능하게끔 위함]<br>
>>
>> ```
>> bool bBool;
>> bool isCan { { get{ return true; } } }
>> ```
>
> ---
>
>> ## 변수
>>
>> 값 할당 시 =의 양쪽 공백 추가<br>
>> 상수 형태로 사용되는 변수는 모든 문자를 대문자로 표기<br>
>> 상수 형태는 보편적으로 public 사용.<br>
>> 상수가 아닌 변수의 외부 접근이 필요한 경우 프로퍼티를 추가 선언<br>
>>
>>> ### 약어
>>>
>>> ID(Identification) 같이 약어를 맨 앞에 표기 시엔 소문자 표기(idList), 그 외 대문자 표기(playerID)<br>
>>>
>>> ```
>>> private int _id;
>>> private int _memberID;
>>> private List<int> _memberIDs;
>>>
>>> private int _gui;
>>> private int _currentGUI;
>>> private List<int> _currentGUIPopups;
>>> ```
>>
>>> ### private, protected `[카멜 표기법]`
>>>
>>> public보다 하단에 선언<br>
>>> 언더스코프 ( _ )를 접두어<br>
>>> 현재 접근하는 변수가 지역변수거나 멤버변수인지 한눈에 분간하기 위함<br>
>>> 인텔리센스 이용 시 _를 입력하면 지역변수를 최상위로 코드 작성에 용이<br>
>>>
>>> ```
>>> private int _foo;
>>> private int _bar;
>>> ```
>>
>>> ### const `[전체 대문자 + 스네이크 표기법]`
>>>
>>> 클래스 최상단에 선언
>>> 보편적으로 public 사용.<br>
>>>
>>> ```
>>> public const int CONST_INDEX = 0;
>>> public static readonly int STATIC_READONLY_INDEX = 0;
>>> ```
>>
>>> ### public `[카멜 표기법]`
>>>
>>> private보다 상단에 선언<br>
>>> struct field, delegate, event, const, static readonly같은 타입이 아니면 사용을 지양<br>
>>>
>>> ```
>>> private int member;
>>> private event Action eventInvoke;
>>> ```
>>
>>> ### 지역변수, 파라미터 `[카멜 표기법]`
>>>
>>> 언더스코프를 ( _ )를 사용하지 않고 표기
>
> ---
>
>> ## Switch
>>
>> switch 내부 case 들여쓰기<br>
>> case가 1줄로 처리가 가능하다면 중괄호를 사용하지 않음<br>
>> case 내용이 2줄 이상일때 중괄호( {} ) 처리<br>
>>
>> ```
>> public void Public()
>> {
>> 	switch ( _id )
>> 	{
>> 		case 0:
>> 			{
>> 			    // ~
>> 			    // ~
>> 			}
>> 			break;
>> 		
>> 		default:
>> 			// ~
>> 			break;          
>> 	}
>> }
>> ```
>
> ---
>
>> ## 열거형 (Enum)
>>
>> 접두어로 e 표기<br>
>> 열거자는 파스칼표기법<br>
>>
>> ```
>> public enum eDirection
>> {
>>     Left,
>>     Right,
>>     Up,
>>     Down,
>> }
>> ```
>>
>> 열거자 탐색을 위해 마지막 열거자를 Max같이 지정하지 않음<br>
>> [C#에서 지원하는 Enum 클래스를 사용하면 해당 열거자의 정보를 가질 수 있으며, Max 없이 순회가 가능]<br>
>>
>> ```
>> public enum eCount
>> {
>>     One,
>>     Two,
>>     Max, // <- 사용하지 말 것
>> }
>> ```
>
> ---
>
>> ## 인터페이스 (interface)
>>
>> 접두어로 I 표기
>>
>> ```
>> public interface IClass
>> {
>>     void Public();
>> }
>> ```

> ## 접근제한자
>
> 접근제한자는 항상 표기<br>
> public, projected를 최대한 지양하며 필요시 Property 활용<br>
>
>> struct의 멤버변수는 보편적으로 public 사용
>>
>> ```
>> public struct Struct
>> {    
>> 	public int index;
>> 	private int _dynamicIndex;
>> }
>> ```
>
>> 외부에서 참조가 불필요한 기능인 경우 private 처리
>>
>> ```
>> public class Foo
>> {
>> 	private void Private()
>> 	{
>> 		// ~Private
>> 	}
>> }
>> ```

> ## 문자열
>
> 문자열을 합칠때 string.Format() 또는 StringBuilder를 사용, C#6이상인 경우 $"{}" 형태로 사용<br>
> `문자열 처리 시 이항 연산자가 매우 비용이 비쌈`<br>
>
>> string.Format() 사용시
>>
>> ```
>> string message = string.Format( "{0}, {1}", foo, bar );
>> ```
>>
>> C# 6.0 이상인 경우
>>
>> ```
>> string message = $"{foo}, {bar}";
>> ```

> ## 프로퍼티
>
> 생성자보다 위에 변수보다 아래 선언<br>
> 단순한 구조인 경우 1줄로 줄여 선언<br>
> `변수와 동일 의미를 가지고 접근하기 때문에 유지보수 편의를 위하여 해당 위치에 작성`<br>
>
>> 중괄호( {} ) 사용 시 공백 추가
>>
>> ```
>> int Age { get { return _age; } }
>> bool isBool { get { return _bBool; } }
>> ```
>>
>> C# 6.0 이상인 경우
>>
>> ```
>> int Age_Csharp6 => _age;
>> bool isBool_Csharp6 => _bBool;
>> ```

> ## var
> 
> 보통 데이터 타입명이 긴편이거나 제네릭 타입이 2개 이상인 충분히 타입이 예상가능한 경우 사용 <br>
> `협업 시엔 가독성 저하로 var 비 선호 개발자가 있을 수 있으므로 최소 사용을 지향`<br>
> 
> ```
> Dictionary<int, float> collection = new Dictionary<int, float>();
> foreach ( var item in collection )
> {
>     // collection의 iterator인 item의 타입은
>     // KeyValuePair<int, float>이나 타입 예상이 가능하므로 사용한 케이스
> }
> ```
> 
> 긴 타입은 var로 선언
> 
> ```
> var instance = new BlaBlaBlaBlaBlaBlaBlaBlaBlaBlaBla();
> ```

> ## 중괄호( {} )
> 
> 새로운 줄에 1개만 사용<br>
> if는 필수적으로 중괄호( {} ) 명시, 다만 return을 처리하는 if는 if( true ) return; 같은 형태로 사용가능<br>
> `여러 처리가 겹칠 경우에 중괄호가 누락되어, 원하지 않는 동작 발생을 방지하기 위해 필수로 정의 하는 것`<br>
> 
> ```
> int max = 10;
> // for문의 경우 ; 앞쪽은 붙여쓰되 뒷쪽은 공백 추가
> for( int i = 0; i < max; i++ )
> {
>     // ~
> }
> ```
> 
>> ### 예외
>>
>> 1줄로 작성 가능한 콜백 및 초기화, 프로퍼티 등 한 단락으로 작성
>>
>> ```
>> Action action = () => {};
>> ```
>>
>> 길어지는 익명함수의 경우 함수 선언부에 중괄호를 시작
>>
>> ```
>> Action action = () => {
>> 	// ~	
>> };
>> ```

> ## 비교 연산
> 
> 상수를 앞으로 배치<br>
> `앞으로 배치하는 이유는 if 내 비교를 대입처리로 오타를 컴파일 단에서 배제 시키기 위함`
> 
> ```
> string text = "text";
> if( "text" == text )
> {
>     // ~
> }
> ```
> 
> Null 체크도 상수처럼 앞쪽에 배치
> 
> ```
> object foo = new object();
> if( null != foo )
> {
>     // ~
> }
> ```
> 
> 크기 비교는 항상 큰값이 오른쪽<br>
> `일관된 방향을 통해 비교하므로 다른 비교처리의 가독성을 높일 수 있음`
> 
> ```
> int min, max;
> if( min <= max )
> {
>     // ~
> } 
> ```