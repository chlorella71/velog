<h1 id="velog와-github를-연동하는-이유">velog와 github를 연동하는 이유</h1>
<ul>
<li><p>github action을 통해서 velog에 포스팅을 할때마다 github의 repository에 push가 되도록 할 수 있다.</p>
</li>
<li><p>이를 활용하면 github의 잔디도 관리할 수 있다.</p>
</li>
</ul>
<h1 id="방법은-다음과-같다">방법은 다음과 같다.</h1>
<h2 id="1-github-actions에서-repository와-velog-연동">1. github actions에서 repository와 velog 연동</h2>
<ul>
<li>github에 velog repository를 생성한다.</li>
<li>repository에 들어간뒤 Actions에 들어간다.</li>
<li>yml로 github repository와 velog를 연동하는 workflows를 작성한다.<ul>
<li>파일경로: .github/workflows/update_blog.yml</li>
</ul>
</li>
</ul>
<ul>
<li>코드:<pre><code>name: Update Blog Posts

</code></pre></li>
</ul>
<p>on:
  push:
      branches:
        - [1.브랜치명]  # 또는 워크플로우를 트리거하고 싶은 브랜치 이름
  schedule:
    # 테스트를 원한다면, <code>한국 표준시 = UTC + 9</code> 참고해서 시간 수정한 후 테스트해보기
    - cron: '0 0 * * *'  # 매일 자정에 실행, UTC 협정 세계시 기준 (한국 시간 기준 오전 9시)
    - cron: '0 15 * * *' # 매일 자정에 실행, 한국 시간 기준 (UTC 15:00)</p>
<p>jobs:
  update_blog:
    runs-on: ubuntu-latest</p>
<pre><code>steps:
- name: Checkout
  uses: actions/checkout@v2

- name: Push changes
  run: |
    git config --global user.name 'github-actions[bot]'
    git config --global user.email 'github-actions[bot]@users.noreply.github.com'
    git push https://${{ secrets.GH_PAT }}@github.com/[2.본인깃허브아이디]/velog.git

- name: Set up Python
  uses: actions/setup-python@v2
  with:
    python-version: '3.x'

- name: Install dependencies
  run: |
    pip install feedparser gitpython

- name: Run script
  run: python scripts/update_blog.py</code></pre><pre><code>- 이때 `[1.브랜치명]`에는 `main` 또는 `master`
  `[2.본인깃허브아이디]`에는 `chlorella71`등 github아이디를 넣으면 된다.
- 코드를 다작성 했으면 `Commit chagnes`버튼을 눌러 commit한다.

## 2. repository에 자동으로 velog post를 push하는 python스크립트 작성
- velog repository에 들어가서 Code &gt; Add file &gt; Create new file
- python script 작성
  - 파일경로: scripts/update_blog.py
- 코드:</code></pre><p>import feedparser
import git
import os</p>
<h1 id="벨로그-rss-피드-url">벨로그 RSS 피드 URL</h1>
<h1 id="example--rss_url--httpsapivelogiorssrimgosu">example : rss_url = '<a href="https://api.velog.io/rss/@rimgosu'">https://api.velog.io/rss/@rimgosu'</a></h1>
<p>rss_url = '<a href="https://api.velog.io/rss/@%5B%EB%B3%B8%EC%9D%B8%EB%B2%A8%EB%A1%9C%EA%B7%B8%EC%95%84%EC%9D%B4%EB%94%94%5D'">https://api.velog.io/rss/@[본인벨로그아이디]'</a></p>
<h1 id="깃허브-레포지토리-경로">깃허브 레포지토리 경로</h1>
<p>repo_path = '.'</p>
<h1 id="velog-posts-폴더-경로">'velog-posts' 폴더 경로</h1>
<p>posts_dir = os.path.join(repo_path, 'velog-posts')</p>
<h1 id="velog-posts-폴더가-없다면-생성">'velog-posts' 폴더가 없다면 생성</h1>
<p>if not os.path.exists(posts_dir):
    os.makedirs(posts_dir)</p>
<h1 id="레포지토리-로드">레포지토리 로드</h1>
<p>repo = git.Repo(repo_path)</p>
<h1 id="rss-피드-파싱">RSS 피드 파싱</h1>
<p>feed = feedparser.parse(rss_url)</p>
<h1 id="각-글을-파일로-저장하고-커밋">각 글을 파일로 저장하고 커밋</h1>
<p>for entry in feed.entries:
    # 파일 이름에서 유효하지 않은 문자 제거 또는 대체
    file_name = entry.title
    file_name = file_name.replace('/', '-')  # 슬래시를 대시로 대체
    file_name = file_name.replace('\', '-')  # 백슬래시를 대시로 대체
    # 필요에 따라 추가 문자 대체
    file_name += '.md'
    file_path = os.path.join(posts_dir, file_name)</p>
<pre><code># 파일이 이미 존재하지 않으면 생성
if not os.path.exists(file_path):
    with open(file_path, 'w', encoding='utf-8') as file:
        file.write(entry.description)  # 글 내용을 파일에 작성

    # 깃허브 커밋
    repo.git.add(file_path)
    repo.git.commit('-m', f'Add post: {entry.title}')</code></pre><h1 id="변경-사항을-깃허브에-푸시">변경 사항을 깃허브에 푸시</h1>
<p>repo.git.push()</p>
<pre><code>- `[본인벨로그아이디]`에는 `chlorella71`처럼 velog아이디 입력
- `Commit changes`로 commit

## 3. github PAT 권한설정
### github token 생성
- github 계정 &gt; Settings
- Developer settings &gt; Personal access tokens &gt; Tokens(classic) &gt; Generate new token &gt; Generate new token(classic)
- Note(토큰이름기입) &amp; Select scopes(repo, workflow 체크) &gt; Generate token
- 생성된 토큰 복사

### repository에 Actions에 token 기입
- velog repository &gt; Settings&gt; Secrets and Variables &gt; Actions &gt; New repository secret
- Name(GH_PAT), Secret(token붙여넣기) &gt; Add secret

### repository에 외부 권한 부여
- velog repository &gt; Settings &gt; Actions &gt; General
- Actions permissions(Allow all actions and reusalbe workflows체크) &gt; Save
- Fork pull request workflows from outside collaborations(Require approval for all external collaborations체크) &gt; Save
- Workflow permissions(Read and write permissions체크, Allow Github Actions to create and approve pull requests체크) &gt; Save

## 4. velog에 포스트시 github에 commit되는지 확인하기

</code></pre>