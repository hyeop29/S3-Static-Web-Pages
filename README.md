# S3-Static-Web-Pages
AWS S3 정적 웹페이지 구성

S3는 쉽게 말하면 클라우드 서비스 내에 있는 외장하드 역할을 한다. 가격이 저렴한 특징을 가지고 있으며,
데이터분석을 위한 기반 시스템의 핵심이기도 한다.
S3는 어떤 파일도 저장할 수 있지만, HTML 파일을 저장시키고 내부기능인 호스팅 기능을 통해 웹 페이지로 전환시켜 보자.

호스팅은 쉽게 설명하면, 서버를 인터넷에서 사용할 수 있도록 URL을 빌려주는 서비스다.
이렇게 하면 내 마음대로 웹에서 서버를 호출 할 수 있다.

정적 호스팅이란, 정적인 웹페이즈를 호스팅한다는 의미입니다.
웹페이지의 내용이 변동적인 것이 아닌, 항상 일정한 것이라면 동적 호스팅보다 비용이 훨씬 저렴한 정적 호스팅 전용 서비스를 사용하는 것이 유리하다.

과제 내용입니다.
1.S3 버킷을 퍼블릭 상태로 구성한다.
2.HTML 파일 3개를 준비한다.
  1) 기본 페이지인 index.html 파일 준비
  2) 에러가 나왔을 때 보여줄 error.html 파일 준비
  3) redirect 기능을 사용해보기 위해 테스트 페이지인 test.html 파일 준비
3. S3 정책 설정
  1) docs 와 documents 폴더 생성 (나중에 URL 뒤에 이 폴더 명을 써주면, 폴더 안에 있는 HTML 파일을 호출한다.)
  2) 호스팅 기능을 켠다
  3) 보안 세부 설정을 위해 정책을 추가
4. 테스트
  1) 기본 페이지를 띄웁니다.
  2) error 상황을 만들어내서 에러페이지를 띄웁니다.
  3) redirect 기능이 잘 작동하는지 테스트
  
  redirect 기능이란 위의 과제는 docs 폴더에는 아무 파일이 없고, documents 폴더에는 test.html이 존재합니다.
  docs 폴더로 들어온 모든 요청을 documents로 변경하도록하는 기능입니다.
  즉 url뒤에 /docs/test.html 을 입력한 url은 redirect 기능이 없다면 error.html 화면이 나오겠지만 이와 같은 설정으로 documents에 있는
  test.html 화면이 나옵니다
  url/docs/test.html 의 호출을 url/documments/test.html 호출로 바꿔준다고 생각하면 됩니다.
  redirect 규칙에 아래의 코드를 입력하면 됩니다.
  
  ```
  [
    { 
      "Condition": { "KeyPrefixEquals": "docs/" },
      "Redirect": { "ReplaceKeyPrefixWith": "documents/" } 
    }
  ]
  ```
  

그 후 과제는 다른 사람이 만든 HTML 파일을 다운로드하여 실행해봤습니다.

https://startbootstrap.com/template/sb-admin
위의 사이트에서 템블릿을 다운받아 실행했습니다.

![image](https://user-images.githubusercontent.com/87464794/215990098-5cf400e4-8c4d-428b-b937-7a54036f1104.png)
실행 결과입니다.
