<h1 id="stream-api">Stream API</h1>
<ul>
<li>java 8에서 도입된 기능으로, 컬렉션(배열, 리스트 등)의 데이터를 <strong>함수형 스타일</strong>로 처리할 수 있도록 도와줌</li>
<li>기존의 <strong>반복문(for, while)을 대체</strong>하여 <strong>간결하고 가독성이 좋은 코드</strong>를 작성할 수 있음</li>
</ul>
<hr />
<h2 id="주요-특징">주요 특징</h2>
<ul>
<li>데이터 처리 전용<ul>
<li>Stream은 데이터 원본(배열, 컬렉션 등)을 변경하지 않고 <strong>새로운 데이터 흐름을 생성</strong></li>
</ul>
</li>
<li>중간 연산(Intermediate Operation)과 최종 연산(Terminal Operation) 구분<ul>
<li>중간 연산: 데이터를 변형 (예: map, filter, sorted)</li>
<li>최종 연산: 데이터를 최종 결과로 반환(예: collect, count, forEach)</li>
</ul>
</li>
<li>병렬 처리 가능 (parallelStream() 활용)<ul>
<li>CPU 코어를 최대한 활용하여 <strong>성능을 최적화</strong>할 수 있음</li>
</ul>
</li>
<li>지연 연산 (Lazy Evaluation)<ul>
<li>최종 연산(collect, forEach 등)이 실행될 때까지 <strong>중간 연산이 실행되지 않음</strong>(불필요한 연산을 줄여 성능 향상)</li>
</ul>
</li>
</ul>
<hr />
<h2 id="stream-사용-예">Stream 사용 예</h2>
<h3 id="1-list에서-stream-생성">1) List에서 Stream 생성</h3>
<pre><code>import java.util.List;
import java.util.stream.Collectors;

public class Main {
    public static void main(String[] args) {
        List&lt;String&gt; names = List.of("apple", "banana", "cherry", "avocado");

        // "a"로 시작하는 문자열만 필터링 후 대문자로 변환하여 리스트로 수집
        List&lt;String&gt; filterNames = names.stream()
            .filter(s -&gt; s.startsWith("a"))    // "a"로 시작하는 단어만 필터링
            .map(String::toUpperCase)    // 대문자로 변환
            .collect(Collectors.toList());    // 결과를 리스트로 변환

        System.out.println(filteredNames);    // 출력: [APPLE, AVOCADO]
    }
}</code></pre><ul>
<li>stream() -&gt; 리스트를 Stream으로 변환</li>
<li>filter(s -&gt; s.startsWith("a")) -&gt; "a"로 시작하는 값만 남김</li>
<li>map(String::toUpperCase) -&gt; 모든 값을 대문자로 변환</li>
<li>collect(Collectors.toList()) -&gt; 리스트로 변환 후 반환</li>
</ul>
<hr />
<h3 id="2-intstream을-활용한-숫자-범위-생성">2) IntStream을 활용한 숫자 범위 생성</h3>
<pre><code>import java.util.stream.IntStream;

public class Main {
    public static void main(String[] args) {
        // 1부터 10까지 숫자 출력
        IntStream.rangeClosed(1, 10)
            .forEach(System.out::println);
    }
}</code></pre><ul>
<li>IntStream.rangeClosed(1, 10) -&gt; <strong>1부터 10까지 반복 (range는 10 제외)</strong></li>
<li>forEach(System.out::println) -&gt; 하나씩 출력</li>
</ul>
<hr />
<h2 id="collectors란">Collectors란?</h2>
<ul>
<li>Collectors는 Stream의 결과를 다양한 형태(리스트, 맵, 문자열 등)로 변환하는 <strong>최종 연산(Terminal Operation)</strong><h3 id="1-리스트로-변환-collectcollectorstolist">1) 리스트로 변환 (collect(Collectors.toList()))</h3>
<pre><code>import java.util.List;
import java.util.stream.Collectors;
</code></pre></li>
</ul>
<p>public class Main
    public static void main(String[] args) {
        List items = List.of("apple", "banana", "cherry");</p>
<pre><code>    List&lt;String&gt; upperCaseItems = items.stream()
        .map(String::toUpperCase)
        .collect(Collectors.toList());

    System.out.println(upperCaseItems);    // [APPLE, BANANA, CHERRY]
}</code></pre><p>}</p>
<pre><code>- collect(Collectors.toList()) -&gt; 리스트로 변환
---
### 2) 문자열 합치기 (collect(Collectors.joining()))</code></pre><p>import java.util.List;
import java.util.stream.Collectors;</p>
<p>public class Main {
    public static void main(String[] args) {
        List words = List.of("Java", "is", "awesome");</p>
<pre><code>    String sentence = words.stream()
        .collect(Collectors.joining(" "));    // 공백을 구분자로 문자열 합치기

    System.out.println(sentence);    // "Java is awesome"
}</code></pre><p>}</p>
<pre><code>- collect(Collectors.joining(" ")) -&gt; "Java is awesome"으로 변환
---
### 3) 그룹화 (collect(Collectors.groupingBy()))</code></pre><p>import java.util.List;
import java.util.Map;
import java.util.stream.Collectors;</p>
<p>public class Main {
    public static void main(String[] args) {
        List items = List.of("apple", "banana", "apricot", "blueberry");</p>
<pre><code>    // 첫 글자를 기준으로 그룹화
    Map&lt;Character, List&lt;String&gt;&gt; grouped = items.stream()
        .collect(Collectors.groupingBy(s -&gt; s.charAt(0)));

    System.out.println(grouped);
    // 출력: {a=[apple, apricot], b=[banana, blueberry]}
}</code></pre><p>}</p>
<pre><code>- collect(Collectors.groupingBy(s -&gt; s.charAt(0)))
  - 첫 글자 기준으로 그룹화 -&gt; **Map&lt;Character, List&gt;** 형태로 변환
---
## Stream과 Collectors 정리
| 기능 | 메서드 |
|-----|------|
| List에서 Stream 생성 | .stream() |
| 배열에서 Stream 생성 | Arrays.stream(arr) |
| 숫자 범위 Stream 생성 | IntStream.range(1, 10) |
| 필터링 (조건에 맞는 요소만 남기기) | .filter(x -&gt; 조건) |
| 변환 (각 요소를 가공) | .map(x -&gt; 새로운 값) |
| 정렬 | .sorted() |
| 중복 제거 | .distinct() |
| 개수 세기 | .count() |
| 합계 계산 (IntStream 전용) | .sum() |
| 평균 계산 (IntStream 전용) | .average() |
| 최댓값 | .max(Comparator.naturalOrder()) |
| 최솟값 | .min(Comparator.naturalOrder()) |
| 리스트로 변환 | .collect(Collectors.toList()) |
| 문자열로 변환 | .collect(Collectors.joining()) |
| 그룹화 | .collect(Collectors.groupingBy()) |
---
## Stream과 Collectors 활용 예제
- 숫자 리스트에서 짝수만 골라서 제곱한 후, 내림차순 정렬하여 리스트로 반환</code></pre><p>import java.util.List;
import java.util.stream.Collectors;
import java.util.stream.IntStream;</p>
<p>public class Main {
    public static void main(String[] args) {
        List result = IntStream.rangeClosed(1, 10)    // 1~10 범위 생성
            .filter(n -&gt; n % 2 == 0)    // 짝수만 선택
            .map(n -&gt; n * n)    // 제곱
            .boxed()    // IntStream -&gt; Stream 변환
            .sorted((a, b) -&gt; b - a)    // 내림차순 정렬
            .collect(Collectors.toList());    // 리스트로 변환</p>
<pre><code>    System.out.println(result);    // [100, 64, 36, 16, 4]
}</code></pre><p>}</p>
<pre><code>---
## 정리
- Stream API는 컬렉션을 **효율적으로 처리하는 함수형 스타일**의 강력한 도구
- Collectors는 Stream의 데이터를 **필요한 형태로 변환**하는 데 사용
- Stream을 사용하면 코드가 **간결, 가독성 증가, 병렬 처리 가능**
- for 문보다 **성능 최적화**에 유리
---
## Stream 클래스 주요 메서드
- Java Stream API에서 자주 사용하는 메서드를 **중간 연산(Intermediate Operations)**과 **최종 연산(Terminal Operations)** 으로 나누어 정리
### 중간 연산 (Intermediate Operations)
- 중간 연산은 데이터 흐름을 변형ㅇ하지만, 최종 연산이 실행될 때까지 실행되지 않음 (Lazy Evaluation)

| 메서드 | 설명 | 예제 |
|------|-----|-----|
| filter(Predicate&lt;T&gt; predicate) | 조건을 만족하는 요소만 필터링 | .filter(n -&gt; n % 2 == 0) |
| map(Function&lt;T, R&gt; mapper) | 요소를 변환 | .map(String::toUpperCase) |
| flatMap(Function&lt;T, Stream&lt;R&gt;&gt; mapper) | 요소를 펼처서 스트림 변환 | .flatMap(s -&gt; Arrays.stream(s.split(""))) |
| distinct() | 중복 제거 | .distinct() |
| sorted() | 오름차순 정렬 | .sorted() |
| sorted(Comparator&lt;T&gt; comparator) | 지정된 비교자로 정렬 | .sorted(Comparator.reverseOrder()) |
| peek(Consumer&lt;T&gt; action) | 요소를 중간에 출력하거나 디버깅 | .peek(System.out::println) |
| limit(long maxSize) | 요소를 제한 | .limit(5) |
| skip(long n) | 처음 n개 요소를 건너뜀 | .skip(3) |
---
### 최종 연산 (Terminal Operations)
- 최종 연산은 Stream을 소비하고 결과를 반환하여 더 이상 사용 불가

| 메서드 | 설명 | 예제 |
|------|-----|-----|
| forEach(Consumer&lt;T&gt; action) | 각 요소에 작업 수행 | .forEach(System.out::println) |
| toArray() | 배열로 반환 | .toArray(String[]::new) |
| count() | 요소 개수 반환 | .count() |
| reduce(BinaryOperator&lt;T&gt; accumulator) | 모든 요소를 하나로 축약 | .reduce((a, b) -&gt; a + b) |
| min(Comparator&lt;T&gt; comparator) | 최솟값 찾기 | .min(Integer::compareTo) |
| max(Comparator&lt;T&gt; comparator) | 최댓값 찾기 | .max(Integer::compareTo) |
| findFirst() | 첫 번째 요소 반환 | .findFirst() |
| findAny() | 임의의 요소 반환 | .findAny() |
| anyMatch(Predicate&lt;T&gt; predicate) | 조건을 만족하는 요소가 하나라도 있는지 검사 | .anyMatch(n -&gt; n &gt; 10) |
| allMatch(Predicate&lt;T&gt; predicate) | 모든 요소가 조건을 만족하는지 검사 | .allMatch(n -&gt; n &gt; 10) |
| noneMatch(Predicate&lt;T&gt; predicate) | 조건을 만족하는 요소가 없는지 검사 | .noneMatch(n -&gt; n &gt; 10) |
---
## Collectors 클래스 주요 메서드
- Collectors는 collect() 최종 연산과 함께 사용되어 데이터를 수집하는데 활용됨

| 메서드 | 설명 | 예제 |
|------|-----|-----|
| toList() | 결과를 List로 변환 | .collect(Collectors.toList()) |
| toSet() | 결과를 Set으로 변환 | .collect(Collectors.toSet()) |
| toMap(Function&lt;T, K&gt; keyMapper, Function&lt;T, U&gt; valueMapper | 결과를 Map으로 변환 | .collect(Collectors.toMap(s -&gt; s.charAt(0), s -&gt; s)) |
| joining() | 문자열을 하나로 합침 | .collect(Collectors.joining()) |
| joining(CharSequence delimiter) | 구분자로 문자열 합침 | .collect(Collectors.joining(", ")) |
| groupingBy(Function&lt;T, K&gt; classifier) | 그룹화하여 Map 반환 | .collect(Collectors.groupingBy(s -&gt; s.length())) |
| partitioningBy(Predicate&lt;T&gt; predicate) | true/false로 구분된 Map&lt;Boolean, List&lt;T&gt;&gt; 반환 | .collect(Collectors.partitioningBy(n -&gt; n % 2 == 0)) |
| counting() | 요소 개수 반환 | .collect(Collectors.counting()) |
| summingInt(ToIntFunction&lt;T&gt; | 요소 합계 반환 | .collect(Collectors.summingInt(Integer::intValue)) |
| averagingInt(ToIntFunction&lt;T&gt; mapper) | 평균값 반환 | .collect(Collectors.averagingInt(Integer::intValue)) |
| maxBy(Comparator&lt;T&gt; comparator) | 최대값 반환 | .collect(Collectors.maxBy(Integer::compareTo)) |
| minBy(Comparator&lt;T&gt; comparator) | 최소값 반환 | .collect(Collectors.minBy(Integer::compareTo)) |
---
## IntStream, LongStream, DoubleStream 주요 메서드
- 기본형 숫자 스트림은 Stream&lt;Integer&gt;보다 성능이 뛰어남

| 메서드 | 설명 | 예제 |
|------|-----|-----|
| range(int start, int end) | start부터 end-1까지 숫자 생성 | IntStream.range(1, 5) -&gt; [1, 2, 3, 4] |
| rangeClosed(int start, int end) | start부터 end까지 숫자 생성 | IntStream.rangeClosed(1, 5) -&gt; [1, 2, 3, 4, 5] |
| of(T... values) | 지정된 값으로 스트림 생성 | IntStream.of(1, 2, 3) |
| iterate(seed, UnaryOperator&lt;T&gt; f) | 초기값부터 함수 적용 | IntStream.iterate(1, n -&gt; n + 2).limit(5) |
| generate(Supplier&lt;T&gt; s) | Supplier 제공값으로 무한 스트림 | IntStream.generate(() -&gt; (int)(Math.random() * 10)).limit(5) |
| sum() | 합계 반환 | IntStream.of(1, 2, 3).sum() |
| average() | 평균 반환 (Optional) | IntStream.of(1, 2, 3).average() |
| max() | 최댓값 반환 (Optional) | IntStream.of(1, 2, 3).max() |
| min() | 최솟값 반환 (Optional) | IntStream.of(1, 2, 3).min() |
---
## 활용 예제
- 짝수만 골라서 제곱 후 합계를 구하기</code></pre><p>import java.util.stream.IntStream;</p>
<p>public class Main {
      public static void main(String[] args) {
          int sum = IntStream.rangeClosed(1, 10)
              .filter(n -&gt; n % 2 == 0)    // 짝수 필터링
              .map(n -&gt; n * n)    // 제곱
              .sum();    // 합계 반환</p>
<pre><code>      System.out.println(sum);    // 220 (2^2 + 4^2 + 6^2 + 8^2 + 10^2)
}</code></pre><p>}</p>
<pre><code>- 리스트에서 문자열 길이 기준 그룹화</code></pre><p>import java.util.List;
import java.util.Map;
import java.util.stream.Collectors;</p>
<p>public class Main {
    public static void main(String[] args) {
          List words = List.of("cat", "dog", "elephant", "tiger", "lion");</p>
<pre><code>    Map&lt;Integer, List&lt;String&gt;&gt; groupedByLength = words.stream()
              .collect(Collectors.groupingBy(String::length));

      System.out.println(groupedByLength);
      // 출력: {3=[cat, dog], 4=[lion], 5=[tiger], 8=[elephant]}
}</code></pre><p>}</p>
<pre><code>---
## 정리
- Stream을 사용하면 **데이터 처리 로직을 간결하고 직관적으로 작성 가능**
- Collectors를 활용하면 **데이터를 원하는 형태(List, Set, Map 등)로 변환 가능**
- 기본형 스트림(IntStream, LongStream)을 사용하면 **성능 최적화 가능**




</code></pre>