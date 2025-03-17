<h1 id="stringbuilderclass">StringBuilder.class</h1>
<ul>
<li>문자열(String)의 수정, 추가 삭제 등을 효율적으로 수행할 수 있도록 설계된 클래스</li>
</ul>
<h2 id="string과-stringbuilder의-차이점">String과 StringBuilder의 차이점</h2>
<table>
<thead>
<tr>
<th>구분</th>
<th>String</th>
<th>StringBuilder</th>
</tr>
</thead>
<tbody><tr>
<td>변경가능여부</td>
<td>불변(Immutable)</td>
<td>가변(Mutable)</td>
</tr>
<tr>
<td>성능</td>
<td>문자열 수정 시 새로운 객체 생성 -&gt; 속도 느림</td>
<td>동일한 객체 내에서 수정 -&gt; 속도 빠름</td>
</tr>
<tr>
<td>메모리 효율성</td>
<td>새로운 객체를 계속 생성하여 메모리 낭비 가능</td>
<td>기존 객체를 변경하므로 메모리 효율적</td>
</tr>
<tr>
<td>스레드 안전성</td>
<td>스레드 안전(final 클래스)</td>
<td>스레드 안전하지 않음</td>
</tr>
<tr>
<td>사용 예시</td>
<td>문자열을 자주 변경하지 않는 경우</td>
<td>문자열을 자주 수정, 추가, 삭제하는 경우</td>
</tr>
</tbody></table>
<ul>
<li><p>문자열을 자주 변경해야한다면 StringBuilder를 사용하는 것이 성능적으로 유리함</p>
</li>
<li><p>멀티스레드 환경에서는 StringBuffer를 사용해야함(StringBuffer는 synchronized 지원)</p>
</li>
<li><p>String을 직접 변강하면 새로운 객체를 계속 생성해야 해서 O(N^2) 시간 복잡도 발생</p>
</li>
<li><p>StringBuilder는 내부에서 하나의 버퍼를 유지하면서 수정하므로 O(N)에 가까운 성능을 제공</p>
</li>
</ul>
<hr />
<h2 id="stringbuilder-기본-사용법">StringBuilder 기본 사용법</h2>
<h3 id="stringbuilder-생성-방법">StringBuilder 생성 방법</h3>
<pre><code>StringBuilder stringBuilder = new StringBuilder("Hello");</code></pre><ul>
<li>기본적으로 StringBuilder는 new 키워드를 사용하여 생성</li>
<li>생성자 초기 문자열을 지정할 수 있고, 빈 객체(new StringBuilder())로 만들 수도 있음</li>
</ul>
<hr />
<h2 id="주요-메서드">주요 메서드</h2>
<table>
<thead>
<tr>
<th>메서드</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>append(String str)</td>
<td>문자열 끝에 추가</td>
</tr>
<tr>
<td>insert(int index, String str)</td>
<td>특정 위치에 문자열 삽입</td>
</tr>
<tr>
<td>delete(int start, int end)</td>
<td>특정 범위 문자 삭제</td>
</tr>
<tr>
<td>reverse()</td>
<td>문자열 뒤집기</td>
</tr>
<tr>
<td>toString()</td>
<td>String으로 변환</td>
</tr>
</tbody></table>
<h3 id="1-append---문자열-추가">1) append() - 문자열 추가</h3>
<pre><code>public class StringBuilderExample {
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder("Hello");
        sb.append(" World");
        System.out.println(sb.toString());    //Hello World
    }
}</code></pre><ul>
<li>append()는 기존 문자열 뒤에 새로운 문자열을 추가</li>
</ul>
<hr />
<h3 id="2-insert---특정-위치에-문자열-삽입">2) insert() - 특정 위치에 문자열 삽입</h3>
<pre><code>public class StringBuilderExample {
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder("Hello");
        sb.insert(5, " World");
        System.out.println(sb.toString());    // Hello Worold
    }
}</code></pre><ul>
<li>지정한 인덱스 위치에 문자열을 삽입</li>
</ul>
<hr />
<h3 id="3-replace---특정-범위-문자열-변경">3) replace() - 특정 범위 문자열 변경</h3>
<pre><code>public class StringBuilderExample {
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder("Hello World");
        sb.replace(6, 11, "Java");
        System.out.println(sb.toSTring());    // Hello Java
    }
}</code></pre><ul>
<li>replac(start, end, "문자열")을 사용하여 특정 구간을 다른 문자열로 교체 가능</li>
</ul>
<hr />
<h3 id="4-delete---특정-문자-삭제">4) delete() - 특정 문자 삭제</h3>
<pre><code>public class StringBuilderExample {
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder("Hello World");
        sb.delete(5, 11);
        System.out.println(sb.toString());    // Hello
    }
}</code></pre><ul>
<li>delete(start, end)를 사용하여 특정 부분의 문자열을 삭제할 수 있음</li>
</ul>
<hr />
<h3 id="5-reverse---문자열-뒤집기">5) reverse() - 문자열 뒤집기</h3>
<pre><code>public class StringBuilderExample {
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder("Hello");
        sb.reverse();
        System.out.println(sb.toString());    //olleH
    }
}</code></pre><ul>
<li>문자열을 뒤집고 싶을때 reverse() 사용</li>
</ul>
<hr />
<h3 id="6-length--capacity---길이와-용량-확인">6) length() &amp; capacity() - 길이와 용량 확인</h3>
<pre><code>public class StringBUilderExample {
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder("Hello");

        System.out.println("Length: " + sb.length());    // 5
        System.out.println("Capacity: " + sb.capacity());    // 기본 16 + 초기 문자열 길이
    }
}</code></pre><ul>
<li>length()는 현재 문자열 길이 반환, capacity()는 내부 버퍼 크기를 반환</li>
<li>기본 용량(capacity)은 16이며, 용량을 초과하면 자동으로 증가</li>
</ul>
<hr />
<h3 id="7-setlength---문자열-길이-설정">7) setLength() - 문자열 길이 설정</h3>
<pre><code>public class StringBuilderExample {
    public static void main(String[] args) {
        StringBuilder sb = new StringBUilder("Hello Wolrd");
        sb.setLength(5);
        System.out.println(sb.toString());    // Hello
    }
}</code></pre><ul>
<li>길이를 줄이면 문자열이 잘리고, 늘리면 빈 공간(\u0000)이 채워짐</li>
</ul>
<hr />
<h2 id="string과-stringbuilder-성능-비교">String과 StringBuilder 성능 비교</h2>
<h3 id="1-string을-사용한-반복문느림">1) String을 사용한 반복문(느림)</h3>
<pre><code>public class StringTest {
    public static void main(String[] args) {
        String str = "";
        for (int i = 0; i&lt; 10000; i++) {
            str += i;    // 새로운 객체가 계쏙 생성됨 -&gt; 비효율적
        |
        System.out.println(str.length());
    }
}</code></pre><ul>
<li>String은 문자열을 변경할 때마다 새로운 객체를 생성하여 메모리 낭비가 발생</li>
<li>시간이 오래 걸림(O(N^2))</li>
</ul>
<hr />
<h3 id="2-stringbuilder를-사용한-반복문빠름">2) StringBuilder를 사용한 반복문(빠름)</h3>
<pre><code>public class StringBuilderTest {
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i &lt; 10000; i++) {
            sb.append(i);    // 동일 객체에서 수정 -&gt; 효율적
        }
        System.out.println(sb.length());
    }
}</code></pre><ul>
<li>StringBuilder는 객체를 새로 생성하지 않고 기존 객체에서 문자열을 변경</li>
<li>성능이 훨씬 빠름 (O(N))</li>
</ul>
<hr />
<h2 id="stringbuilder-vs-stringbuffer">StringBuilder vs StringBuffer</h2>
<table>
<thead>
<tr>
<th>구분</th>
<th>StringBuilder</th>
<th>StringBuffer</th>
</tr>
</thead>
<tbody><tr>
<td>동작 방식</td>
<td>가변 문자열 (빠름)</td>
<td>가변 문자열 (멀티스레드 안전)</td>
</tr>
<tr>
<td>스레드 안전성</td>
<td>X (멀티스레드 X)</td>
<td>O (멀테스레드 O)</td>
</tr>
<tr>
<td>성능</td>
<td>더 빠름</td>
<td>상대적으로 느림</td>
</tr>
<tr>
<td>사용 상황</td>
<td>단일 스레드</td>
<td>멀티 스레드</td>
</tr>
</tbody></table>
<ul>
<li>멀티 스레드 환경에서는 StringBuffer 사용, 일반적인 경우에는 더 빠른 StringBuilder 사용</li>
</ul>
<hr />
<h2 id="stringbuilder를-사용할-때">StringBuilder를 사용할 때</h2>
<ul>
<li><p>문자열을 자주 변경해야하는 경우 (append(), delete(), replace())</p>
</li>
<li><p>반복문에서 문자열을 연결해야 할 때 (for 루프 안에서 append())</p>
</li>
<li><p>성능이 중요한 경우 (String보다 훨씬 빠름)</p>
</li>
<li><p>멀티 스레드 환경에서는 StringBuffer, 단일 스레드에서는 StringBuilder를 사용하면 최적의 성능을 얻을 수 있음</p>
</li>
</ul>