<h1 id="throwable">Throwable</h1>
<ul>
<li>Throwable은 <strong>java에서 예외(Exception)와 에러(Error)를 모두 포함하는 최상위 클래스</strong></li>
<li><strong>모든 예외와 오류는 Throwable을 상속받은 클래스임</strong></li>
</ul>
<hr />
<h2 id="throwable의-계층-구조">Throwable의 계층 구조</h2>
<ul>
<li>java의 예외와 오류는 <strong>Throwable을 기반으로 두가지로 나뉨</strong><pre><code>Object
└── Throwable    &lt;- 모든 예외(Exception)와 에러(Error)의 부모 클래스
  ├── Exception    &lt;- 예외 (Checked &amp; Unchecked Exception)
  │   ├── IOException
  │   ├──SQLException
  │   ├── RuntimeException (Unchecked Exception)
  │   │   ├── NullPointerException
  │   │   ├── ArithmeticException
  │   │   ├── ArrayIndexOutOfBoundsException
  │   │   └── ...
  │   └── ...
  └── Error        &lt;- 시스템 오류 (JVM 관련 오류)
      ├── OutOfMemoryError
      ├── StackOverflowError
      ├── VirtualMachineError
      ├── AssertionError
      └── ...</code></pre></li>
<li><strong>Throwable의 두 가지 주요 하위 클래스</strong><ul>
<li><strong>Exception -&gt; 예외(프로그램에서 발생하는 오류)</strong>, 개발자가 직접 처리 가능</li>
<li><strong>Error -&gt; 시스템 오류(JVM 관련 문제)</strong>, 개발자가 직접 처리하지 않음</li>
</ul>
</li>
</ul>
<hr />
<h2 id="throwable의-주요-메서드">Throwable()의 주요 메서드</h2>
<ul>
<li><p>Throwable의 클래스는 예외를 다룰 때 유용한 메서드를 제공함</p>
<h3 id="1-printstacktrace---예외의-발생-원인을-출력">1) printStackTrace() - 예외의 발생 원인을 출력</h3>
<pre><code>try {
  int result = 10 / 0;
} catch (Throwable t) {
  t.printStackTrace();
}</code></pre></li>
<li><p>출력 예시 (ArithmeticException 발생):</p>
<pre><code>java.lang.ArithmeticException: / by zero
  at Main.main(Main.java:4)</code></pre><ul>
<li>예외가 발생한 위치와 원인을 알 수 있음</li>
</ul>
</li>
</ul>
<hr />
<h3 id="2-getmessage---예외-메시지-가져오기">2) getMessage() - 예외 메시지 가져오기</h3>
<pre><code>try {
    int num = Integer.parseInt("abc");
} catch (Throwable t) {
    System.out.println("예외 메시지: " + t.getMessage());
}</code></pre><ul>
<li>출력 결과 (NumberFormatException):<pre><code>예외 메시지: For input string: "abc"</code></pre><ul>
<li>예외가 발생한 이유를 알 수 있음</li>
</ul>
</li>
</ul>
<hr />
<h3 id="3-getcause---예외의-원인-가져오기">3) getCause() - 예외의 원인 가져오기</h3>
<pre><code>try {
    throw new RuntimeException("런타임 오류", new NullPointerException("원인 예외"));
} catch (Throwable t) {
    System.out.println("예외 원인: " + t.getCause());
}</code></pre><ul>
<li>출력 결과:<pre><code>예외 원인: java.lang.NullPointerException: 원인 예외</code></pre><ul>
<li>다른 예외를 원인으로 포함할 수도 있음</li>
</ul>
</li>
</ul>
<hr />
<h2 id="throwable과-exception의-차이">Throwable과 Exception의 차이</h2>
<table>
<thead>
<tr>
<th>비교 항목</th>
<th>Throwable</th>
<th>Exception</th>
</tr>
</thead>
<tbody><tr>
<td>부모 클래스</td>
<td>Object</td>
<td>Throwable</td>
</tr>
<tr>
<td>하위 클래스</td>
<td>Exception, Error</td>
<td>IOException, RuntimeException, SQLException 등</td>
</tr>
<tr>
<td>용도</td>
<td>예외 + 오류 포함</td>
<td>예외 처리 (프로그램 오류)</td>
</tr>
<tr>
<td>catch로 잡을 수 있음?</td>
<td>가능</td>
<td>가능</td>
</tr>
</tbody></table>
<hr />
<h2 id="throwable의-catch-사용">Throwable의 catch 사용</h2>
<ul>
<li><p>Throwable을 catch하면 <strong>모든 예외(Exception)와 시스템 오류(Error)를 잡을 수 있음</strong></p>
</li>
<li><p>그러나 <strong>보통 Exception만 잡고, Error는 잡지 않는 것이 좋음</strong></p>
</li>
<li><p>잘못된 사용 (Error까지 잡음)</p>
<pre><code>try {
  int num = 10 / 0;
} catch (Throwable t) {    // Error도 포함해서 잡음
  System.out.println("예외 발생: " + t.getMessage());
}</code></pre></li>
<li><p>올바른 사용 예시 (Exception만 잡기)</p>
<pre><code>try {
  int num = 10 / 0;
} catch (Exception e)    // 일반적인 예외만 잡음
  System.out.println("예외 발생: " + e.getMessage());
}</code></pre></li>
</ul>
<hr />
<h2 id="error를-catch하면-안되는-이유">Error를 catch하면 안되는 이유</h2>
<ul>
<li><p><strong>Error는 시스템 레벨에서 발생하는 치명적인 오류이므로, 개발자가 직접 처리하는 것이 적절하지 않음</strong></p>
</li>
<li><p>예로, <strong>OutOfMemoryError</strong>(메모리 부족 오류)가 발생하면, 이를 잡아도 해결할 방법이 없음</p>
<pre><code>try {
  long[] memoryLeak = new long[Integer.MAX_VALUE];    // 너무 큰 배열 할당시 OutOfMemoryError 발생
} catch (Error e) {    // 절대 Error를 잡지 말 것
  System.out.println("시스템 오류 발생: " + e.getMessage());
}</code></pre></li>
<li><p>출력 결과 (OutOfMemeoryError)</p>
<pre><code>Exception in thread "main" java.lang.OutOfMemoryError: Requested array size exceeds VM limit</code></pre><ul>
<li>시스템 오류(Error)는 catch로 처리하지 않고, 프로그램을 종료하는 것이 적절함</li>
</ul>
</li>
</ul>
<hr />
<h2 id="정리">정리</h2>
<table>
<thead>
<tr>
<th>개념</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>Throwable</td>
<td>Exception과 Error의 최상위 부모 클래스</td>
</tr>
<tr>
<td>Exception</td>
<td>프로그램 실행 중 발생하는 예외 (개발자가 직접 처리 가능)</td>
</tr>
<tr>
<td>RuntimeException</td>
<td>실행 중(Runtime)에 발생하는 예외(NullPointerException, ArithmeeticException 등)</td>
</tr>
<tr>
<td>Error</td>
<td>시스템 오류 (OutOfMemoryError, StackOverflowError 등), 개발자가 직접 처리하지 않음</td>
</tr>
<tr>
<td>Throwable을 catch하는 것</td>
<td>모든 예외와 시스템 오류를 잡을 수 있지만, 일반적으로 권장되지 않음</td>
</tr>
<tr>
<td>Error를 잡으면 안 되는 이유</td>
<td>시스템 오류는 해결할 수 없고, 프로그램을 종료하는 것이 더 적절함</td>
</tr>
</tbody></table>
<ul>
<li>결론: Throwable은 예외와 오류의 최상위 부모 클래스지만, 일반적으로 Excpetion만 처리하고 Error는 처리하지 않는 것이 좋음</li>
</ul>