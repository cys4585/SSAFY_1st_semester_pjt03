# pjt03 - 반응형 웹페이지 구성하기





### 1. 목표

- HTML을 통한 웹페이지 마크업 분석
- CSS 라이브러리의 이해와 활용
- 컴포넌트 및 그리드 시스템 활용
- 커뮤니티 서비스 반응형 레이아웃 구성





### 2. 준비사항

 	1. 개발도구
      	1. Visual Studio Code
      	2. Google Chrome Browser
      	3. Bootstrap v5.0
 	2. 제공 Assets
     - images/
       - 사용할 이미지들
     - 01_nav_footer.html
       - 모든 페이지가 공유할 Navigation bar 및 Footer
     - 01_nav_footer.css
     - 02_home.html
       - 사용자가 처음 접속하면 보게될 페이지
     - 02_home.css
     - 03_community.html
       - 사용자들끼리 의견을 나누는 게시판
     - 03_community.css
	3. 요구사항
    - README.pdf 참고





### 3. 구현 내용



##### A. 01_nav_footer

1. Navigation Bar

   1. 브라우저 상단에 고정

      - nav 태그에 fixed-top class 활용

   2. 로고이미지 images/logo.png 사용, 클릭가능한 링크, 02_home.html 페이지로 연결

   3. 네비게이션 리스트(Home, Community, Login)는 ul과 li 사용

      - ul 태그에 list-unstyled  class 활용(li 앞의 '-'을 없애줌)

   4. 로고이미지는 좌상단, 네비게이션 리스트는 우상단에 표시

      - nav 태그에 d-flex, justify-content-between, align-items-center class 활용

   5. Home - 02_home.html / Community - 03_community.html 링크연결

      - li 태그 안에 a태그 선언
      - href의 value로 링크주소 입력
      - a 태그에 text-decoration-none 활용(text의 밑줄을 없애줌)

   6. Home 강조

      - Home에만 text-light / Community, Login에는 text-secondary class 활용(text color 변경)

   7. Login 클릭시 Modal 컴포넌트를 통하여 로그인 창 띄어짐 (페이지 이동 x)

      - Bootstrap 공식 홈페이지 Docs에 Modal 검색 후 copy paste
      - 연결해야할 a태그에 data-bs-target="# modal의 id"를 넣으면 a태그와 modal 컴포넌트가 연결됨
      - 세부 내용은 간단히 커스터마이징 가능함 (form 태그, label 태그, submit button)

   8. Viewport의 가로 크기가 768px(md) 미만일 경우 네베이게이션 리스트가 햄버거 버튼으로 교체, 클릭시 세부 항목 활성화

      - 햄버거 아이콘은
        - Bootstrap icon 홈페이지에서 지원하는 icon 사용 (cdn 및 icon 태그 copy&paste)
        - button 태그안에 icon 태그 넣어주면 클릭 가능
        - Bootstrap 홈페이지 docs에서 navbar 검색후 가장 밑을 보면 햄버거 버튼 사용 관련한 코드 있음
          - data-bs-target과 대상 id를 맞추면 연결됨

      - ul 태그 class에 d-none, d-md-flex를 주면
        - 기본적으로는 ul 태그가 display: none;이 주어지면서 공간할당이 취소되고, 가로크기가 md(768px)가 넘어가는 경우 display: flex;가 주어지면서 다시 공간을 할당받음
      - 반대로 button 태그 class에 d-md-none을 주면
        - 가로크기가 md(768px)이 넘어가는 경우 display: none;이 주어지면서 공간할당이 취소됨
      - 햄버거 버튼을 클릭하면 열리는 div태그 역시 d-md-none을 주면 동일 효과 가능

1. Footer
   1. 브라우저 하단 고정
      - footer 태그 class에 fixed-bottom
   2. 수평 정렬(왼쪽, 오른족 여백 동일)
      - footer 태그 class에 d-flex, fustify-content-center

```html
<!-- 01_nav_footer.html -->

<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <!-- Bootstrap CSS -->
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-giJF6kkoqNQ00vy+HMDP7azOuL0xtbfIcaT9wjKHr8RbDVddVHyTfAAsrekwKmP1" crossorigin="anonymous">
  <!-- Custom CSS -->
  <link rel="stylesheet" href="01_nav_footer.css">
  <!-- Bootstrap icon -->
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.3.0/font/bootstrap-icons.css">
  <title>Navbar Footer Test</title>
</head>
<body>
  <!-- 01_nav_footer.html -->

  <!-- navbar -->
  <nav class="fixed-top d-flex justify-content-between bg-dark text-light align-items-center px-2 py-2">
    <a href="02_home.html"><img src="images/logo.png" alt=""></a>
    <ul class="list-unstyled d-flex m-0 justify-content-end d-none d-md-flex">
      <li class="mx-3"><a class="text-decoration-none text-light" href="02_home.html">Home</a></li>
      <li class="mx-3"><a class="text-decoration-none text-secondary" href="03_community.html">Community</a></li>
      <li class="mx-3"><a class="text-decoration-none text-secondary" href="#" data-bs-toggle="modal" data-bs-target="#login">Login</a></li>
    </ul>
    <button class="btn d-inline-block d-md-none text-secondary fs-2 p-0 m-0" data-bs-toggle="collapse" data-bs-target="#navbarToggleExternalContent" aria-controls="navbarToggleExternalContent" aria-expanded="false" aria-label="Toggle navigation">
      <i class="bi bi-list d-flex align-self-center"></i>
    </button>
  </nav>
  <div class="collapse d-md-none" id="navbarToggleExternalContent" style="margin-top: 50px;">
    <div class="bg-dark">
      <ul class="list-unstyled">
        <li class="p-2"><a class="text-decoration-none text-light" href="02_home.html">Home</a></li>
        <li class="p-2"><a class="text-decoration-none text-secondary" href="03_community.html">Community</a></li>
        <li class="p-2"><a class="text-decoration-none text-secondary" href="#" data-bs-toggle="modal" data-bs-target="#login">Login</a></li>
      </ul>
    </div>
  </div>

  <!-- modal (login) -->
  <div class="modal fade" id="login" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">Login</h5>
          <button class="btn-close" type="button" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body">
          <form id="login-form">
            <div class="mb-3">
              <label for="exampleInputEmail1" class="form-label">Username</label>
              <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
            </div>
            <div class="mb-3">
              <label for="exampleInputPassword1" class="form-label">Password</label>
              <input type="password" class="form-control" id="exampleInputPassword1">
            </div>
            <div class="mb-3 form-check">
              <input type="checkbox" class="form-check-input" id="exampleCheck1">
              <label class="form-check-label" for="exampleCheck1">Check me out</label>
            </div>
            <hr>
            <div class="d-flex justify-content-end">
              <button type="button" class="btn btn-secondary m-1" data-bs-dismiss="modal">Close</button>
              <button type="submit" class="btn btn-primary m-1">Submit</button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>

  <!-- footer -->
  <footer class="fixed-bottom d-flex justify-content-center text-secondary">
    <p>Web-bootstrap PJT, by Youngsu Choi</p>
  </footer>

  <!-- Bootstrap JS -->
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta1/dist/js/bootstrap.bundle.min.js" integrity="sha384-ygbV9kiqUc6oa4msXn9868pTtWMgiQaeYH7/t7LECLbyPA2x65Kgf80OJFdroafW" crossorigin="anonymous"></script>
</body>
</html>

```

```css
/* 01_nav_footer.css */

nav {
  height: 50px;
}

nav > a > img {
  width: 100px;
}
```



##### B. 02_home

1. Navigation Bar & Footer
   1. 01_nav_footer.html에서 copy & paste
   2. Home 강조
2. Header
   1. 이미지 자동 전환 (images/ 폴더 밑의 header 이미지 사용)
      - Bootstrap Docs에서 carousel 검색
      - 코드 copy & paste
      - img태그의 src 수정
3. Section
   1. Section 내부의 개별 요소(article)들 일정한 간격으로 떨어뜨리기
      - Bootstrap Docs에서 card 검색
      - 코드 copy & paste
      - section 태그 class에 px-5 => x축(left, right) padding: 3rem
   2. Viewport 가로크기 576px 미만인 경우 한 열(row)에 article 요소 하나씩 표시
      - section 태그 class에 row-cols-1
   3. Viewport 가로크기 576px 이상인 경우 한 열(row)에 article 요소 2개 이상 자유롭게 표시
      - section 태그 class에
        - row-cols-sm-2
        - row-cols-md-3
        - row-cols-lg-4
        - row-cols-xxl-5

```html
<!-- 02_home.html -->

<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <!-- Bootstrap CSS -->
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-giJF6kkoqNQ00vy+HMDP7azOuL0xtbfIcaT9wjKHr8RbDVddVHyTfAAsrekwKmP1" crossorigin="anonymous">
  <!-- Custom CSS -->
  <link rel="stylesheet" href="01_nav_footer.css">
  <link rel="stylesheet" href="02_home.css">
  <!-- Bootstrap icon -->
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.3.0/font/bootstrap-icons.css">
  <title>Home</title>
</head>
<body>

  <!-- 01_nav_footer.html -->
  <!-- 01_nav_footer 에서 완성한 Navigation bar 코드를 붙여넣어 주세요. -->
    <!-- navbar -->
    <nav class="fixed-top d-flex justify-content-between bg-dark text-light align-items-center px-2 py-2">
      <a href="02_home.html"><img src="images/logo.png" alt=""></a>
      <ul class="list-unstyled d-flex m-0 justify-content-end d-none d-md-flex">
        <li class="mx-3"><a class="text-decoration-none text-light" href="02_home.html">Home</a></li>
        <li class="mx-3"><a class="text-decoration-none text-secondary" href="03_community.html">Community</a></li>
        <li class="mx-3"><a class="text-decoration-none text-secondary" href="#" data-bs-toggle="modal" data-bs-target="#login">Login</a></li>
      </ul>
      <button class="btn d-inline-block d-md-none text-secondary fs-2 p-0 m-0" data-bs-toggle="collapse" data-bs-target="#navbarToggleExternalContent" aria-controls="navbarToggleExternalContent" aria-expanded="false" aria-label="Toggle navigation">
        <i class="bi bi-list d-flex align-self-center"></i>
      </button>
    </nav>
    <div class="collapse  d-md-none" id="navbarToggleExternalContent" style="margin-top: 50px;">
      <div class="bg-dark">
        <ul class="list-unstyled">
          <li class="p-2"><a class="text-decoration-none text-light" href="02_home.html">Home</a></li>
          <li class="p-2"><a class="text-decoration-none text-secondary" href="03_community.html">Community</a></li>
          <li class="p-2"><a class="text-decoration-none text-secondary" href="#" data-bs-toggle="modal" data-bs-target="#login">Login</a></li>
        </ul>
      </div>
    </div>
  
    <!-- modal (login) -->
    <div class="modal fade" id="login" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">Login</h5>
            <button class="btn-close" type="button" data-bs-dismiss="modal" aria-label="Close"></button>
          </div>
          <div class="modal-body">
            <form id="login-form">
              <div class="mb-3">
                <label for="exampleInputEmail1" class="form-label">Username</label>
                <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
              </div>
              <div class="mb-3">
                <label for="exampleInputPassword1" class="form-label">Password</label>
                <input type="password" class="form-control" id="exampleInputPassword1">
              </div>
              <div class="mb-3 form-check">
                <input type="checkbox" class="form-check-input" id="exampleCheck1">
                <label class="form-check-label" for="exampleCheck1">Check me out</label>
              </div>
              <hr>
              <div class="d-flex justify-content-end">
                <button type="button" class="btn btn-secondary m-1" data-bs-dismiss="modal">Close</button>
                <button type="submit" class="btn btn-primary m-1">Submit</button>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
  

  <!-- 02_home.html -->
  <header style="margin-top: 50px;">
    <div id="carouselExampleIndicators" class="carousel slide" data-bs-ride="carousel">
      <ol class="carousel-indicators">
        <li data-bs-target="#carouselExampleIndicators" data-bs-slide-to="0" class="active"></li>
        <li data-bs-target="#carouselExampleIndicators" data-bs-slide-to="1"></li>
        <li data-bs-target="#carouselExampleIndicators" data-bs-slide-to="2"></li>
      </ol>
      <div class="carousel-inner">
        <div class="carousel-item active">
          <img src="images/header1.jpg" class="d-block w-100" alt="...">
        </div>
        <div class="carousel-item">
          <img src="images/header2.jpg" class="d-block w-100" alt="...">
        </div>
        <div class="carousel-item">
          <img src="images/header3.jpg" class="d-block w-100" alt="...">
        </div>
      </div>
      <a class="carousel-control-prev" href="#carouselExampleIndicators" role="button" data-bs-slide="prev">
        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
        <span class="visually-hidden">Previous</span>
      </a>
      <a class="carousel-control-next" href="#carouselExampleIndicators" role="button" data-bs-slide="next">
        <span class="carousel-control-next-icon" aria-hidden="true"></span>
        <span class="visually-hidden">Next</span>
      </a>
    </div>
  </header>

  <h1 class="d-flex justify-content-center mt-5 mb-4 fw-bold">Boxoffice</h1>

  <section class="row row-cols-1 row-cols-sm-2 row-cols-md-3 row-cols-lg-4 row-cols-xxl-5 g-4 px-5">
    <article class="col">
      <div class="card">
        <img src="images/movie1.jpg" class="card-img-top" alt="...">
        <div class="card-body">
          <h5 class="card-title">Movie title</h5>
          <p class="card-text">This is a longer card with supporting text below as a natural lead-in to additional content. This content is a little bit longer.</p>
        </div>
      </div>
    </article>
    <article class="col">
      <div class="card">
        <img src="images/movie2.jpg" class="card-img-top" alt="...">
        <div class="card-body">
          <h5 class="card-title">Movie title</h5>
          <p class="card-text">This is a longer card with supporting text below as a natural lead-in to additional content. This content is a little bit longer.</p>
        </div>
      </div>
    </article>
    <article class="col">
      <div class="card">
        <img src="images/movie3.jpg" class="card-img-top" alt="...">
        <div class="card-body">
          <h5 class="card-title">Movie title</h5>
          <p class="card-text">This is a longer card with supporting text below as a natural lead-in to additional content. This content is a little bit longer.</p>
        </div>
      </div>
    </article>
    <article class="col">
      <div class="card">
        <img src="images/movie4.jpg" class="card-img-top" alt="...">
        <div class="card-body">
          <h5 class="card-title">Movie title</h5>
          <p class="card-text">This is a longer card with supporting text below as a natural lead-in to additional content. This content is a little bit longer.</p>
        </div>
      </div>
    </article>
    <article class="col">
      <div class="card">
        <img src="images/movie5.jpg" class="card-img-top" alt="...">
        <div class="card-body">
          <h5 class="card-title">Movie title</h5>
          <p class="card-text">This is a longer card with supporting text below as a natural lead-in to additional content. This content is a little bit longer.</p>
        </div>
      </div>
    </article>
    <article class="col">
      <div class="card">
        <img src="images/movie6.jpg" class="card-img-top" alt="...">
        <div class="card-body">
          <h5 class="card-title">Movie title</h5>
          <p class="card-text">This is a longer card with supporting text below as a natural lead-in to additional content. This content is a little bit longer.</p>
        </div>
      </div>
    </article>

  </section>

  <!-- 01_nav_footer.html -->
  <!-- 01_nav_footer 에서 완성한 Footer 코드를 붙여넣어 주세요. -->
    <!-- footer -->
    <footer class="fixed-bottom d-flex justify-content-center text-secondary">
      <p>Web-bootstrap PJT, by Youngsu Choi</p>
    </footer>

    
  <!-- Bootstrap JS -->
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta1/dist/js/bootstrap.bundle.min.js" integrity="sha384-ygbV9kiqUc6oa4msXn9868pTtWMgiQaeYH7/t7LECLbyPA2x65Kgf80OJFdroafW" crossorigin="anonymous"></script>
</body>
</html>
```



##### C. 03_community

1. Navigation Bar & Footer 
   1. copy & paste
   2. Community 강조
      - Community => text-light / Home, Login => text-secondary
2. 게시판 목록 & 게시판
   1. div.container 생성 및 그 안에 div.row 2개 생성
   2. 첫번째 row에 div.col-12 생성 및 그 안에 Community h1 태그 삽입
   3. 두번째 row에 aside 태그(게시판 목록) & section 태그 생성(게시판)
   4. aside
      1. .col-12 .col-lg-2
         - default로 12/12칸 차지, 992px 이상인 경우 2/12칸 차지
      2. aside 안에 ul.list-group 생성
         - li.list-group-item.list-group-item-action 생성 * 4
           - 각 li 안에 a.text-decoration-none 및 안에 내용text삽입 (Boxoffice, Movies, Genres, Actors)
   5. section
      1. .col-12.col-lg-10
         - default로 12/12칸 차지, 992px 이상인 경우 10/12칸 차지
           - 10/12칸 차지하게되면 aside와 section은 같은 div.row에 있기때문에 aside 오른쪽에 section이 위치함
      2. section 안에 div 2개 생성
         1. div 2개 생성 이유 : Viewport의 가로크기에 따라 Browser에 보이는 게시판 구성을 바꾸기 위해
            - 첫번째 div => div.d-none.d-lg-block
              - default로 공간할당 X, 992px 이상이되면 display: block으로 공간 할당
              - table(표) 요소로 표시
            - 두번째 div => div.d-block.d-lg-none
              - default로 display: block, 992px 이상이되면 공간할당 X
              - article 태그들로 표시
         2. table => Bootstrap Docs에서 table 검색후 copy & paste (table.table.table-striped)
            1. thead.bg-dark.text-light
               - th * 4 (영화제목, 글제목, 작성자, 작성시간)
            2. tbody
               - tr(row) / td(column)
         3. article => article.d-flex.flex-column
            1. hr
            2. div.d-flex.justify-content-between
               - 글 제목
               - 작성자
            3. div 영화 제목
            4. div 작성시간
      3. 게시판 Pagination (Page Navigation)
         1. div.col-12 => 항상 12/12칸을 할당했기 때문에 한 줄 전체를 차지함 (게시판 section 안에 있는 요소이기 때문에 게시판과 항상 같은 가로폭을 가짐)
            - article.d-flex.justify-content.center => 메인축(가로축) 중앙 정렬
              - Bootstrap docs에서 pagination 검색 및 copy & paste
              - ul.pagination
                - li.page-item * 5
                - a.page-link
                  - Previous / 1 / 2 / 3 / Next

```html
<!-- 03_community.html -->

<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <!-- Bootstrap CSS -->
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-giJF6kkoqNQ00vy+HMDP7azOuL0xtbfIcaT9wjKHr8RbDVddVHyTfAAsrekwKmP1" crossorigin="anonymous">
  <!-- Custom CSS -->
  <link rel="stylesheet" href="01_nav_footer.css">
  <link rel="stylesheet" href="03_community.css">
  <!-- Bootstrap icon -->
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.3.0/font/bootstrap-icons.css">
  <title>Community</title>
</head>
<body>

  <!-- 01_nav_footer.html -->
  <!-- 01_nav_footer 에서 완성한 Navigation bar 코드를 붙여넣어 주세요. -->
    <!-- navbar -->
    <nav class="fixed-top d-flex justify-content-between bg-dark text-light align-items-center px-2 py-2">
      <a href="02_home.html"><img src="images/logo.png" alt=""></a>
      <ul class="list-unstyled d-flex m-0 justify-content-end d-none d-md-flex">
        <li class="mx-3"><a class="text-decoration-none text-secondary" href="02_home.html">Home</a></li>
        <li class="mx-3"><a class="text-decoration-none text-light" href="03_community.html">Community</a></li>
        <li class="mx-3"><a class="text-decoration-none text-secondary" href="#" data-bs-toggle="modal" data-bs-target="#login">Login</a></li>
      </ul>
      <button class="btn d-inline-block d-md-none text-secondary fs-2 p-0 m-0" data-bs-toggle="collapse" data-bs-target="#navbarToggleExternalContent" aria-controls="navbarToggleExternalContent" aria-expanded="false" aria-label="Toggle navigation">
        <i class="bi bi-list d-flex align-self-center"></i>
      </button>
    </nav>
    <div class="collapse  d-md-none" id="navbarToggleExternalContent" style="margin-top: 50px;">
      <div class="bg-dark">
        <ul class="list-unstyled">
          <li class="p-2"><a class="text-decoration-none text-secondary" href="02_home.html">Home</a></li>
          <li class="p-2"><a class="text-decoration-none text-light" href="03_community.html">Community</a></li>
          <li class="p-2"><a class="text-decoration-none text-secondary" href="#" data-bs-toggle="modal" data-bs-target="#login">Login</a></li>
        </ul>
      </div>
    </div>
  
    <!-- modal (login) -->
    <div class="modal fade" id="login" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">Login</h5>
            <button class="btn-close" type="button" data-bs-dismiss="modal" aria-label="Close"></button>
          </div>
          <div class="modal-body">
            <form id="login-form">
              <div class="mb-3">
                <label for="exampleInputEmail1" class="form-label">Username</label>
                <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
              </div>
              <div class="mb-3">
                <label for="exampleInputPassword1" class="form-label">Password</label>
                <input type="password" class="form-control" id="exampleInputPassword1">
              </div>
              <div class="mb-3 form-check">
                <input type="checkbox" class="form-check-input" id="exampleCheck1">
                <label class="form-check-label" for="exampleCheck1">Check me out</label>
              </div>
              <hr>
              <div class="d-flex justify-content-end">
                <button type="button" class="btn btn-secondary m-1" data-bs-dismiss="modal">Close</button>
                <button type="submit" class="btn btn-primary m-1">Submit</button>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>


  <!-- 03_community.html -->
  <div class="main container p-4" style="margin-top: 50px;">
    <div class="row">
      <div class="col-12 text-center p-4">
        <h1 class="fw-bold" style="font-size: 2.5rem;">Community</h1>
      </div>
    </div>
    
    <div class="row">
      <!-- Sidebar -->
      <aside class="col-12 col-lg-2 my-2">
        <ul class="list-group">
          <li class="list-group-item list-group-item-action p-3"><a href="#" class="text-decoration-none">Boxoffice</a></li>
          <li class="list-group-item list-group-item-action p-3"><a href="#" class="text-decoration-none">Movies</a></li>
          <li class="list-group-item list-group-item-action p-3"><a href="#" class="text-decoration-none">Genres</a></li>
          <li class="list-group-item list-group-item-action p-3"><a href="#" class="text-decoration-none">Actors</a></li>
        </ul>
      </aside>
      
      <!-- Board -->
      <section class="col-12 col-lg-10 my-2">
        <div class="d-none d-lg-block">
          <table class="table table-striped">
            <thead class="bg-dark text-light">
              <th>영화 제목</th>
              <th>글 제목</th>
              <th>작성자</th>
              <th>작성 시간</th>
            </thead>
            <tbody>
              <tr>
                <td>Great Movie title</td>
                <td>Best Movie Ever</td>
                <td>user</td>
                <td>1 minutes ago</td>
              </tr>
              <tr>
                <td>Great Movie title</td>
                <td>Movie Test</td>
                <td>user</td>
                <td>1 minutes ago</td>
              </tr>
              <tr>
                <td>Great Movie title</td>
                <td>Movie Test</td>
                <td>user</td>
                <td>1 minutes ago</td>
              </tr>
              <tr>
                <td>Great Movie title</td>
                <td>Movie Test</td>
                <td>user</td>
                <td>1 minutes ago</td>
              </tr>
              <tr>
                <td>Great Movie title</td>
                <td>Movie Test</td>
                <td>user</td>
                <td>1 minutes ago</td>
              </tr>
              <tr>
                <td>Great Movie title</td>
                <td>Movie Test</td>
                <td>user</td>
                <td>1 minutes ago</td>
              </tr>
              <tr>
                <td>Great Movie title</td>
                <td>Movie Test</td>
                <td>user</td>
                <td>1 minutes ago</td>
              </tr>
              <tr>
                <td>Great Movie title</td>
                <td>Movie Test</td>
                <td>user</td>
                <td>1 minutes ago</td>
              </tr>
              <tr>
                <td>Great Movie title</td>
                <td>Movie Test</td>
                <td>user</td>
                <td>1 minutes ago</td>
              </tr>
            </tbody>
          </table>
        </div>
        <div class="d-block d-lg-none">
          <hr>
          <article class="d-flex flex-column px-4">
            <div class="d-flex justify-content-between">
              <p class="my-1 fs-5">Best Movie Ever</p>
              <p class="my-1">user</p>
            </div>
            <div><p class="my-1">Great Movie Title</p></div>
            <div><p class="my-1">1 minutes ago</p></div>
          </article>

          <hr>
          <article class="d-flex flex-column px-4">
            <div class="d-flex justify-content-between">
              <p class="my-1 fs-5">Movie Test</p>
              <p class="my-1">user</p>
            </div>
            <div><p class="my-1">Great Movie Title</p></div>
            <div><p class="my-1">1 minutes ago</p></div>
          </article>
          
          <hr>
          <article class="d-flex flex-column px-4">
            <div class="d-flex justify-content-between">
              <p class="my-1 fs-5">Movie Test</p>
              <p class="my-1">user</p>
            </div>
            <div><p class="my-1">Great Movie Title</p></div>
            <div><p class="my-1">1 minutes ago</p></div>
          </article>
        </div>
        
        <div class="col-12 my-5">
          <article class="d-flex justify-content-center">
            <nav aria-label="Page navigation example">
              <ul class="pagination">
                <li class="page-item"><a class="page-link" href="#">Previous</a></li>
                <li class="page-item"><a class="page-link" href="#">1</a></li>
                <li class="page-item"><a class="page-link" href="#">2</a></li>
                <li class="page-item"><a class="page-link" href="#">3</a></li>
                <li class="page-item"><a class="page-link" href="#">Next</a></li>
              </ul>
            </nav>
          </article>
        </div>
      </section>
    </div>
    
  </div>
  <!-- 01_nav_footer.html -->
  <!-- 01_nav_footer 에서 완성한 Footer 코드를 붙여넣어 주세요. -->
  <!-- footer -->
  <footer class="fixed-bottom d-flex justify-content-center text-secondary">
    <p>Web-bootstrap PJT, by Youngsu Choi</p>
  </footer>


  <!-- Bootstrap JS -->
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta1/dist/js/bootstrap.bundle.min.js" integrity="sha384-ygbV9kiqUc6oa4msXn9868pTtWMgiQaeYH7/t7LECLbyPA2x65Kgf80OJFdroafW" crossorigin="anonymous"></script>
</body>
</html>
```



