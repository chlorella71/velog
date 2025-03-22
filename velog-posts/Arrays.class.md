<h1 id="arrays-클래스javautilarrays란">Arrays 클래스(java.util.Arrays)란?</h1>
<ul>
<li>Arrays 클래스는 배열을 다룰 때 유용한 메서드들을 제공하는 유틸리티 클래스임</li>
<li>java.util.Arrays 패키지에 퐇마되어 있으며, Import java.util.Arrays;를 통해 사용할 수 있음</li>
</ul>
<hr />
<h2 id="주요-기능-및-메서드">주요 기능 및 메서드</h2>
<table>
<thead>
<tr>
<th>메서드</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>toString(arr)</td>
<td>배열을 문자열로 변환 (예: [1, 2, 3])</td>
</tr>
<tr>
<td>deepToString(arr)</td>
<td>다차원 배열을 문자열로 변환</td>
</tr>
<tr>
<td>copyOf(arr, newLength)</td>
<td>배열 복사 및 크기 변경</td>
</tr>
<tr>
<td>copyOfRange(arr, start, end)</td>
<td>특정 범위의 배열 복사</td>
</tr>
<tr>
<td>fill(arr, value)</td>
<td>배열을 특정 값으로 채우기</td>
</tr>
<tr>
<td>sort(arr)</td>
<td>배열 정렬 (기본 오름차순)</td>
</tr>
<tr>
<td>binarySearch(arr, key)</td>
<td>정렬된 배열에서 이진 탐색 수행</td>
</tr>
<tr>
<td>equals(arr1, arr2)</td>
<td>두 배열이 동일한지 비교</td>
</tr>
<tr>
<td>deepEquals(arr1, arr2)</td>
<td>다차원 배열이 동일한지 비교</td>
</tr>
<tr>
<td>asList(arr)</td>
<td>배열을 List로 변환</td>
</tr>
<tr>
<td>stream(arr)</td>
<td>배열을 Stream으로 변환 (Java 8+)</td>
</tr>
</tbody></table>
<hr />
<h2 id="1-tostring---배열을-문자열로-변환">1) toString() - 배열을 문자열로 변환</h2>
<ul>
<li>1차원 배열 출력<pre><code>import java.util.Arrays;
</code></pre></li>
</ul>
<p>public class Main {
    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5};</p>
<pre><code>    System.out.println(Arrays.toString(arr));
    // 출력: [1, 2, 3, 4, 5]
}</code></pre><p>}</p>
<pre><code>
- 2차원 배열 출력</code></pre><p>import java.util.Arrays;</p>
<p>public class Main {
    public static void main(String[] args) {
        int[][] arr = {{1, 2, 3}, {4, 5, 6}};</p>
<pre><code>    System.out.println(Arrays.toString(arr));    // 주소값 출력
    System.out.println(Arrays.deepToString(arr));    // [ [1, 2, 3], [4, 5, 6] ]
}</code></pre><p>}</p>
<pre><code>- 1차원 배열은 Arrays.toString() 사용, 2차원 배열은 Arrays.deeptoString()을 사용해야 함
---
## copyOf() &amp; copyOfRange() - 배열 복사
- 배열 크기 늘리기 (copyOf)</code></pre><p>import java.util.Arrays;</p>
<p>public class Main {
    public static void main(String[] args) {
        int[] arr = {1, 2, 3];</p>
<pre><code>    int[] newArr = Arrays.copyOf(arr, 5);    // 크기 5로 확장 (빈 공간은 0으로 채움)

    System.out.println(Arrays.toString(newArr));    // [1, 2, 3, 0, 0]
}</code></pre><p>}</p>
<pre><code>- 기존 배열보다 크기가 크면 0으로 채워짐 (기본형 기준)
---
- 배열 일부 목사 (copyOfRange)</code></pre><p>import java.util.Arrays;</p>
<p>public class Main {
    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5};</p>
<pre><code>    int[] subArr = Arrays.copyOfRange(arr, 1, 4);    // 인덱스 1~3 복사 (4번 인덱스 제외)

    System.out.println(Arrays.toString(subArr));    // [2, 3, 4]
}</code></pre><p>}</p>
<pre><code>- end 인덱스는 포함되지 않음
---
## fill() - 배열을 특정 값으로 채우기</code></pre><p>import java.util.Arrays;</p>
<p>public class Main {
    public static void main(String[] args) {
        int[] arr = new int[5];</p>
<pre><code>    Arrays.fill(arr, 7);

    System.out.println(Arrays.toString(arr));    // [7, 7, 7, 7, 7, 7]
}</code></pre><p>}</p>
<pre><code>- 모든 요소를 7로 채움
---
## sort() - 배열 정렬
- 기본 정렬 (오름차순)</code></pre><p>import java.util.Arrays;</p>
<p>public class Main {
    public static void main(String[] args) {
        int[] arr = {5, 3, 8, 1, 2};</p>
<pre><code>    Arrays.sort(arr);

    System.out.println(Arrays.toString(arr));    // [1, 2, 3, 5, 8]
}</code></pre><p>}</p>
<pre><code>
- 내림차순 정렬 (객체 배열)</code></pre><p>import java.util.Arrays;
import java.util.Collections;</p>
<p>public class Main {
    public static void main(String[] args) {
        Integer[] arr = {5, 3, 8, 1, 2};</p>
<pre><code>    Arrays.sort(arr, Collections.reverseOrder());

    System.out.println(Arrays.toString(arr));
}</code></pre><p>}</p>
<pre><code>- int[] 는 reverseOrder()를 사용할 수 없으므로 Integer[]를 사용해야 함
---
## binarySearch() - 이진 탐색 (정렬 필수)</code></pre><p>import java.util.Arrays;</p>
<p>public class Main {
    public static void main(String[] args) {
        int[] arr = {2, 4, 6, 8, 10};</p>
<pre><code>    int index = Arrays.binarySearch(arr, 6);

    System.out.println(index);    // 출력: 2 (인덱스 2에 위치)
}</code></pre><p>}</p>
<pre><code>- 이진 탐색을 하기 전에 Arrays.sort()로 정렬이 되어 있어야 함
---
## equals() &amp; deepEquals() - 배열 비교
- 1차원 배열 비교</code></pre><p>import java.util.Arrays;</p>
<p>public class Main {
    public static void main(String[] args) {
        int[] arr1 = {1, 2, 3};
        int[] arr2 = {1, 2, 3};</p>
<pre><code>    System.out.println(Arrays.equals(arr1, arr2));    // true
}</code></pre><p>}</p>
<pre><code>
- 2차원 배열 비교 (deepEquals 필수)</code></pre><p>import java.util.Arrays;</p>
<p>public class Main {
    public static void main(String[] args) {
        int[][] arr1 = {{1, 2}, {3, 4}};
        int[][] arr2 = {{1, 2}, {3, 4}};</p>
<pre><code>    System.out.println(Arrays.equals(arr1, arr2));    // false (주소 비교)
    System.out.println(Arrays.deepEquals(arr1, arr2));    // true (내용 비교)
}</code></pre><p>}</p>
<pre><code>---
## asList() - 배열을 리스트로 변환</code></pre><p>import java.util.Arrays;
import java.util.List;</p>
<p>public class Main {
    public static void main(String[] args) {
        String[] arr = {&quot;apple&quot;, &quot;banana&quot;, &quot;cherry&quot;};</p>
<pre><code>    List&lt;String&gt; list = Arrays.asList(arr);

    System.out.println(list);    // [apple, banana, cherry]
}</code></pre><p>}</p>
<pre><code>- 배열을 리스트로 변환하여 List 메서드 사용 가능
  - 하지만 크기 변경(추가/삭제)은 불가능! (ArrayList로 변환해야 함)
---
## stream() - 배열을 Stream으로 변환 (Java 8+)</code></pre><p>import java.util.Arrays;
import java.util.stream.IntStream;</p>
<p>public class Main {
    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5};</p>
<pre><code>    IntStream stream = Arrays.stream(arr);
    stream.forEach(System.out::println);
}</code></pre><p>}</p>
<p>```</p>
<ul>
<li>스트림을 활용하여 람다식과 함께 사용 가능</li>
</ul>
<hr />
<h2 id="정리">정리</h2>
<table>
<thead>
<tr>
<th>메서드</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>toString()</td>
<td>배열 출력</td>
</tr>
<tr>
<td>copyOf()</td>
<td>배열 크기 변경</td>
</tr>
<tr>
<td>sort()</td>
<td>정렬</td>
</tr>
<tr>
<td>binarySearch()</td>
<td>이진 탐색</td>
</tr>
<tr>
<td>equals()</td>
<td>배열 비교</td>
</tr>
<tr>
<td>asList()</td>
<td>리스트 변환</td>
</tr>
<tr>
<td>stream()</td>
<td>스트림 변환</td>
</tr>
<tr>
<td>- 배열을 다룰 때 Arrays 클래스는 매우 유용하므로 익숙해지면 좋음</td>
<td></td>
</tr>
</tbody></table>