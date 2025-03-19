<h1 id="exception예외">Exception(예외)</h1>
<ul>
<li><strong>예외(Exception)</strong>는 프로그램 실행 중에 발생하는 비정상적인 상황</li>
<li>예외가 발생하면 프로그램이 <strong>비정상적으로 종료될 수 있음</strong>, 이를 <strong>적절히 처리(예외 처리, Exception Handling)</strong> 해야함</li>
</ul>
<hr />
<h2 id="예외의-종류">예외의 종류</h2>
<ul>
<li>java는 예외를 크게 <strong>Checked Exception(체크 예외)</strong>과 <strong>Unchecked Exception(언체크 예외)</strong>로 구분<h3 id="1-checked-exception-컴파일러가-체크하는-예외">1) Checked Exception (컴파일러가 체크하는 예외)</h3>
</li>
<li><strong>컴파일 시점</strong>에 반드시 예외 처리를 해야하는 예외</li>
<li>try-catch 또는 throws를 사용해야 컴파일이 가능</li>
<li>네트워크, 파일 I/O, 데이터베이스 관련 예외들이 포함됨<h4 id="예제-ioexception">예제 (IOException):</h4>
<pre><code>import java.io.*;
</code></pre></li>
</ul>
<p>class CheckedExceptionExample {
    public static void main(String[] args) {
        try {
            FileReader file = new FileReader("test.txt");    // 파일이 없으면 예외 발생
        } catch (FileNotFoundException e) {
            System.out.println("파일을 찾을 수 없습니다.");
        }
    }
}</p>
<pre><code>- FileReader를 사용할 때, FileNotFoundException을 반드시 처리해야함
---
### 2) Unchecked Exception (컴파일러가 체크하지 않는 예외)
- 실행 중(Runtime)에 발생하는 예외 (컴파일 시 예외 처리 강제 X)
- **개발자가 직접 방어 코드 작성해야 함**
- 대부분 **프로그래밍 로직 오류(Null, Index 범위 초과, 형 변환 오류 등)** 와 관련됨
#### 예제 (NullPointerException, ArithmeticException):</code></pre><p>class UncheckedExceptionExample {
    public static void main(String[] args) {
        String str = null;
        System.out.println(str.length());    // NullPointerException 발생
    }
}</p>
<pre><code>- null 체크 없이 str.length()를 호출했기 때문에 NullPonterException 발생
---
## 주요 예외 종류
### Checked Exception
| 예외 클래스 | 설명 |
|----------|-----|
| IOException | 입출력 관련 예외 (파일 읽기, 쓰기 오류 등) |
| SQLException | 데이터베이스 관련 예외 |
| ClassNotFoundExceptio | 클래스 로딩 실패 |
| InterruptedException | 스레드 인터럽트 예외 |

### UnChecked Exception
| 예외 클래스 | 설명 |
|----------|-----|
| NullPointerException | null 값을 참조할 때 발생 |
| ArrayIndexOutOfBoundsException | 배열의 인덱스를 초과할 때 발생 |
| ArithmeticException | 0으로 나누는 연산에서 발생(/ by zero) |
| ClassCastException | 잘못된 형 변환에서 발생 |
| NumberFormatException | 문자열을 숫자로 변환할 때 발생 (Integer.parseInt("abc")) |
---
## 예외 처리 방법
- java에서는 **예외 처리를 위해 try-catch, throws, finally를 사용**할 수 있음
### 1) try-catch를 사용한 예외 처리</code></pre><p>class TryCatchExample {
    public static void main(String[] args) {
        try {
            int result = 10 / 0; // ArithmeticException 발생
        } catch (ArithmeticException e) {
            System.out.println("0으로 나눌 수 없습니다.");
        }
    }
}</p>
<pre><code>- 예외 발생 시, 프로그램이 종료되지 않고 정상적으로 처리됨
---
### 2) throws를 사용한 예외 처리 (예외를 호출자에게 위임)</code></pre><p>class ThrowsExample {
    public static void riskyMethod() throws ArithmeticException {
        int result = 10 / 0;    // ArithmeticException 발생
    }</p>
<pre><code>public static void main(String[] args) {
    try {
        riskyMethod();
    } catch (ArithmeticException e) {
        System.out.println("예외 발생: " + e.getMessage());
    }
}</code></pre><p>}</p>
<pre><code>- throws를 사용하면, 예외 처리 main()에서 수행할 수도 있음
---
### 3) finally 블록 (예외 발생 여부와 관계없이 실행)
- finally 블록은 **예외가 발생하든 안 하든 반드시 실행됨**
- **파일 닫기, 리소스 정리, 데이터베이스 연결 해제 등의 작업**에서 많이 사용됨</code></pre><p>class FinallyExample {
    public static void main(String[] args) {
        try {
            int result = 10 / 2;
            System.out.println("결과: " + result);
        } catch (ArithmeticException e) {
            System.out.println("예외 발생: " + e.getMessage());
        } finally {
            System.out.println("예외 여부와 관계없이 실행됨");
        }
    }
}</p>
<pre><code>- finally 블록은 예외가 발생하든 안 하든 항상 실행됨
---
## 사용자 정의 예외 (Custom Exception)
- Java에서는 Exception 클래스를 상속받아 **사용자 정의 예외(Custom Exception)** 를 만들 수도 있음</code></pre><p>class MyException extends Exception {    // Checked Exception
    public MyException(String message) {
        super(message);
    }
}</p>
<p>class CustomExceptionExample {
    public static void main(String[] args) {
        try {
            throw new MyException("사용자 정의 예외 발생");
        } catch (MyException e) {
            System.out.println(e.getMessage());
        }
    }
}</p>
<pre><code>- MyException을 직접 정의하며, 특정 상황에서 예외를 발생시킬 수 있음
---
## 예외 처리 Best Practice
### 1) try-catch는 최소 범위로 적용</code></pre><p>// 잘못된 예시: try 범위가 너무 넓음
try {
    System.out.println("작업1");
    int result = 10 / 0;
    System.out.println("작업2");
} catch (ArithmeticException e) {
    System.out.println("예외 발생");
}</p>
<p>// 올바른 예시: 필요한 부분만 try-catch 사용
System.out.println("작업1");
try {
    int result = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println("예외 발생");
}
System.out.println("작업2");</p>
<pre><code>### 2) catch 블록에서 너무 많은 예외를 처리하지 않기</code></pre><p>// 잘못된 예시: 너무 많은 예외를 한 번에 처리
try {
    int result = 10 / 0;
    String s = null;
    System.out.println(s.length());
} catch (Exception e) {    // 모든 예외를 한 번에 처리하면 원인 파악이 어려움
    System.out.println("예외 발생");
}</p>
<p>// 올바른 예시: 개별 예외 처리
try {
    int result = 10 / 0;<br />} catch (ArithmeticException e) {
    System.out.println("산술 연산 예외 발생");
} catch (NullPointerException e) {
    System.out.println("널 포인터 예외 발생");
}</p>
<h2 id="">```</h2>
<h2 id="정리">정리</h2>
<table>
<thead>
<tr>
<th>개념</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>Checked Exception</td>
<td>컴파일 시 예외 처리가 강제됨 (IOException, SQLException 등)</td>
</tr>
<tr>
<td>Unchecked Exception</td>
<td>실행 중 발생하는 예외 (NullPointerException, ArrayIndexOutofBoundsException 등)</td>
</tr>
<tr>
<td>try-catch</td>
<td>예외를 잡아서 프로그램이 종료되지 않도록 처리</td>
</tr>
<tr>
<td>throws</td>
<td>예외를 호출자에게 넘김</td>
</tr>
<tr>
<td>finally</td>
<td>예외 발생 여부와 관계없이 실행</td>
</tr>
<tr>
<td>사용자 정의 예외</td>
<td>Exception을 상속받아 직접 예외 클래스를 생성</td>
</tr>
</tbody></table>
<h3 id="핵심-요약">핵심 요약</h3>
<ul>
<li>try-catch로 예외 처리하면 프로그램이 멈추지 않음</li>
<li>throws를 사용하면 예외를 호출자에게 넘길 수 있음</li>
<li>finally는 항상 실행됨 (리소스 정리용)</li>
<li><strong>예외 처리는 최소한으로, 필요한 부분만 적용하는 것이 중요</strong></li>
</ul>