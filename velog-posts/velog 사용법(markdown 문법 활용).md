<h1 id="velog-기본-문법">velog 기본 문법</h1>
<p>velog는 마크다운 문법 사용
마크다운(markdown)문법이란?
<a href="https://namu.wiki/w/%EB%A7%88%ED%81%AC%EB%8B%A4%EC%9A%B4">마크다운문법</a></p>
<hr />
<h2 id="1-제목">1. 제목</h2>
<p>h1부터 h6으로 제목 표현
벨로그에서는 제목을 통해 목차를 알아서 생성해줌</p>
<p>마크다운 작성시</p>
<pre><code># h1
## h2
### h3
#### h4
##### h5
###### h6</code></pre><h1 id="h1">h1</h1>
<h2 id="h2">h2</h2>
<h3 id="h3">h3</h3>
<h4 id="h4">h4</h4>
<h5 id="h5">h5</h5>
<h6 id="h6">h6</h6>
<p>📌**h1과 h2는 이렇게도 작성 가능</p>
<pre><code>h1
==
h2
--
하이픈(-) 여러개
----</code></pre><h1 id="h1-1">h1</h1>
<h2 id="h2-1">h2</h2>
<h2 id="하이픈--여러개">하이픈(-) 여러개</h2>
<hr />
<h2 id="2-인라인-코드블록-만들기">2. 인라인 코드블록 만들기</h2>
<p>한줄짜리 코드블럭은 ``을 이용하여 작성</p>
<pre><code>`인라인 코드`</code></pre><p>엔터 후 탭 2번으로도 가능</p>
<pre><code>    인라인코드</code></pre><pre><code>코드블록은 백틱( ` )으로 감싸서 작성함
여러줄은 ``` 여러줄 ```, 또는 ~~~ 여러줄 ~~~로 사용
첫번째 ```줄 옆에 java, python 등을 언어 이름을 적으면 적용됨
</code></pre><pre><code class="language-java">public class HelloWorld {
public void main(String[] agrs) {
    //hello world
    System.out.println("Hello World");
    }
}</code></pre>
<hr />
<h2 id="3-인용문">3. 인용문</h2>
<p>문단 맨 앞에 <code>&gt;</code>을 씀</p>
<blockquote>
<p>예시</p>
<blockquote>
<p>중첩인용문</p>
</blockquote>
</blockquote>
<hr />
<h2 id="4-링크-삽입">4. 링크 삽입</h2>
<p>인라인 링크 작성
<code>[인라인 링크이름](httlp://velog.io/)</code>
<a href="https://www.google.com">Google</a></p>
<p>uri 링크 작성
<code>&lt;https://velog.io/&gt;</code></p>
<hr />
<h2 id="5-이미지-삽입">5. 이미지 삽입</h2>
<p><code>![이미지 설명](이미지 링크)</code>형태로 작성
<img alt="Google" src="https://upload.wikimedia.org/wikipedia/commons/c/c1/Google_%22G%22_logo.svg" /></p>
<p>이미지에 링크 추가
<code>[![이미지설명](이미지링크)](연결하고자하는 url "마우스오버시 나타낼 링크 title")</code>
<a href="https://ko.m.wikipedia.org/wiki/%ED%8C%8C%EC%9D%BC:Google_%22G%22_logo.svg"><img alt="Google" src="https://upload.wikimedia.org/wikipedia/commons/c/c1/Google_%22G%22_logo.svg" /></a></p>
<hr />
<h2 id="6-이모지">6. 이모지</h2>
<p>아래주소의 이모지를 복사+붙여넣기로 사용하면 됨
<a href="http://kr.piliapp.com/twitter-symbols/">http://kr.piliapp.com/twitter-symbols/</a></p>
<pre><code>단축키
윈도우: w + .
맥북: control + command + spacebar</code></pre><p>😇</p>
<hr />
<h2 id="7-수평선">7. 수평선</h2>
<p><code>-</code>또는 <code>*</code>또는 <code>_</code>를 3개 이상 작성
(단, <code>-</code>를 사용할 경우 header로 인식할 수 있어 이 전 라인은 비워야함)</p>
<hr />
<hr />
<hr />
<hr />
<h2 id="8-문단">8. 문단</h2>
<p>문단과 문단 사이는 빈줄(엔터키 두번)로 구분</p>
<pre><code>1문단


2문단</code></pre><p>1문단</p>
<p>2문단</p>
<p><code>&lt;br/&gt;</code>활용가능</p>
<pre><code>1문단&lt;br/&gt;&lt;br/&gt;
2문단</code></pre><p>1문단<br /><br />
2문단</p>
<hr />
<h2 id="9-목록리스트">9. 목록(리스트)</h2>
<h3 id="91-순서있는-목록번호">9.1 순서있는 목록(번호)</h3>
<p>순서있는 목록은 숫자와 점을 사용</p>
<pre><code>1. 첫번째
2. 두번째
3. 세번째</code></pre><ol>
<li>첫번쨰</li>
<li>두번째</li>
<li>세번째</li>
</ol>
<hr />
<h3 id="92-순서없는-목록글머리기호">9.2 순서없는 목록(글머리기호)</h3>
<pre><code>* 첫번째 
  * 두번째
    * 세번째
+ 첫번째
  + 두번째
    + 세번째
- 첫번째
  - 두번째
    - 세번째</code></pre><ul>
<li><p>첫번째</p>
<ul>
<li>두번쨰<ul>
<li>세번째</li>
</ul>
</li>
</ul>
</li>
<li><p>첫번째</p>
<ul>
<li>두번쨰<ul>
<li>세번째</li>
</ul>
</li>
</ul>
</li>
<li><p>첫번째</p>
<ul>
<li>두번째<ul>
<li>세번째</li>
</ul>
</li>
</ul>
</li>
</ul>
<p><del>velog에서는 마크다운문법이 100% 적용이 되지는 않는 것 같기도 함</del>
📌tab은 적용이 안되고 spacebar 2번은 적용됨</p>
<hr />
<h2 id="10-강조폰트스타일">10. 강조(폰트스타일)</h2>
<p>굵게, 기울이기, 취소선 등 기본적인 스타일을 작성할 수 있음</p>
<pre><code>*기울여쓰기*
_기울여쓰기_
**굵게쓰기**
__굵게쓰기__
~~취소선~~</code></pre><hr />
<h2 id="11-테이블">11. 테이블</h2>
<p>테이블은 |(파이프)로 구분, 기본적인 폰트스타일(굵게, 기울임, 취소선)적용 가능
-(하이픈)으로 구분된 곳 각각 왼쪽, 양쪽, 오른쪽에 :(세미콜론)을 붙일 경우 순서대로 왼쪽, 가운데, 오른쪽 정렬 가능</p>
<pre><code>| 드라마 제목 | 주연 배우 | 방영일 |
|:---|:---:|---:|
|:---왼쪽정렬|:---:가운데정렬|---:오른쪽정렬|
|**호텔 델루나**| _이지은, 여진구_ | ~~2019.07.13 ~ 2019.09.01~~|</code></pre><p>| 드라마 제목 | 주연 배우 | 방영일 |
|:---왼쪽정렬|<del>:---:가운데정렬</del>|---:오른쪽정렬|
<del>velog에서는 가운데정렬까지는 안되는 것 같음</del></p>
<table>
<thead>
<tr>
<th align="left">드라마제목</th>
<th align="center">주연배우</th>
<th align="right">방영일</th>
</tr>
</thead>
<tbody><tr>
<td align="left"><strong>호텔 델루나</strong></td>
<td align="center"><em>이지은, 여진구</em></td>
<td align="right"><del>2019.07.13 ~ 2019.09.01</del></td>
</tr>
<tr>
<td align="left"><strong>타인은 지옥이다</strong></td>
<td align="center"><em>임시완, 이동욱, 이현욱, 이정은</em></td>
<td align="right"><del>2019.08.31 ~</del></td>
</tr>
</tbody></table>
<p>📌마크다운 테이블을 쉽게 만들 수 있는 사이트가 있음
<a href="https://www.tablesgenerator.com/markdown_tables">TablesGenerator</a>
<img alt="TablesGenerator" src="https://velog.velcdn.com/images/chlorella71/post/3e9f9181-029f-45bf-9449-71d2bb4727f9/image.png" /></p>
<p>📌테이블 내에서 파이프기호를 사용하고 싶으면 html문법을 활용하면됨</p>
<pre><code>| : &amp;#124;
코드를 작성하고 싶으면
&lt;code&gt;&amp;#124;&lt;/code&gt;</code></pre><hr />
<h2 id="12-체크박스">12. 체크박스</h2>
<p><code>-</code>,<code>*</code>,<code>+</code>뒤에 띄어쓰기 후 <code>대괄호</code>를 넣어 작성
<code>대괄호</code>안에 띄어쓰기 : 빈 체크박스
<code>대괄호</code>안에 <code>x</code>를 넣으면 체크된 체크박스</p>
<pre><code>- [ ] 운동하기
- [x] 강의듣기</code></pre><ul>
<li><input disabled="" type="checkbox" /> 운동하기</li>
<li><input checked="" disabled="" type="checkbox" /> 강의듣기</li>
</ul>
<p><del>[x]는 velog에서 안되는 것 같음</del></p>
<hr />
<h2 id="13-글자색상">13. 글자색상</h2>
<p>html태그를 이용하여 작성가능</p>
<pre><code class="language-html">&lt;span style="color:red"&gt;red&lt;/span&gt;
&lt;span style="color:#d3d3d3"&gt;#d3d3d3&gt;&lt;/span&gt;
&lt;span style="color:rgb(245, 235, 13)"&gt;rgb(245, 235, 13)&lt;/span&gt;</code></pre>
<p><span style="color: red;">red</span>
<span style="color: #d3d3d3;">#d3d3d3&gt;</span>
<span style="color: rgb(245, 235, 13);">rgb(245, 235, 13)&gt;</span></p>
<hr />
<p>참고사이트</p>
<ul>
<li><a href="https://velog.io/@jinuku/Velog-%EA%B0%84%EB%8B%A8-%EC%82%AC%EC%9A%A9%EB%B2%95">https://velog.io/@jinuku/Velog-%EA%B0%84%EB%8B%A8-%EC%82%AC%EC%9A%A9%EB%B2%95</a></li>
<li><a href="https://velog.io/@yeseolee/Velog-%EC%82%AC%EC%9A%A9%EB%B2%95-%EC%A0%95%EB%A6%AC">https://velog.io/@yeseolee/Velog-%EC%82%AC%EC%9A%A9%EB%B2%95-%EC%A0%95%EB%A6%AC</a></li>
<li><a href="https://dullyshin.github.io/2019/02/25/Hexo-MarkdownTable/">https://dullyshin.github.io/2019/02/25/Hexo-MarkdownTable/</a></li>
</ul>