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

  <footer class="fixed-bottom d-flex justify-content-center text-secondary">
    <p>Web-bootstrap PJT, by Youngsu Choi</p>
  </footer>

  <!-- Bootstrap JS -->
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta1/dist/js/bootstrap.bundle.min.js" integrity="sha384-ygbV9kiqUc6oa4msXn9868pTtWMgiQaeYH7/t7LECLbyPA2x65Kgf80OJFdroafW" crossorigin="anonymous"></script>
</body>
</html>

```

