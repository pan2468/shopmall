## 📌 쇼핑몰 프로젝트
+ JpaRepository 인터페이스 CRUD 메소드 이용하여 상품관리, 구매이력, 장바구니 기능 구현
+ QueryDSL 객체지향 쿼리를 이용하여 검색조건 구현
+ SpringSecurity 설정
+ UserDetailsService 로그인 인증 구현

### 👉 제작기간, 참여인원
+ 제작기간: 2022.05.10 ~ 2022.05.15
+ 참여인원: 개인프로젝트
### 🛠 사용기술 (기술스택)
+ Java 11
+ SpringBoot 2.7.0
+ Spring Security
+ Spring Data JPA
+ QueryDSL 5.0.0
+ Maven
+ MySQL
## 👉 시퀀스 다이어그램

## 👉 서비스 화면

<details>
<summary><b>쇼핑몰 프로세스 화면</b></summary>
<div markdown="1">

<details>
<summary><b>로그인</b></summary>
<div markdown="2">
	
<img src="https://user-images.githubusercontent.com/58936137/180049925-15194daf-d78d-4402-a48c-30da56db3bb3.png" width="750px" height="450px">

### 로그인 인증
+ email, password 입력을 합니다.
+ SpringSecurity 보안프레임워크에서 UserDetailsService 사용하여 로그인 인증
</div>
</details>

<details>
<summary><b>회원 가입</b></summary>
<div markdown="2">
	<img src="https://user-images.githubusercontent.com/58936137/180049754-499d18ee-37ec-4c2b-91a3-3c869f5b1cd1.png" width="750px" height="450px">

### 회원가입 insert
+ 이름, 이메일 주소, 비밀번호, 주소를 입력합니다.
+ JpaRepository 인터페이스 save() 메소드를 이용하여 등록하여 INSERT 삽입합니다. 

</div>
</details>

<details>
<summary><b>메인 페이지</b></summary>
<div markdown="2">
	<img src="https://user-images.githubusercontent.com/58936137/180047764-3856a741-86e4-4f15-8344-eb117458f4d7.png" width="750px" height="450px">
	
### 메인페이지 
+ 로그인 인증 성공시 redirect:/ 메인 페이지로 이동합니다.
+ admin 로그인시 상품등록, 상품관리 메뉴가 링크 호출이 됩니다. 
</div>
</details>

<details>
<summary><b>상품 등록</b></summary>
<div markdown="2">
	<img src="https://user-images.githubusercontent.com/58936137/180048894-e95a367c-3537-4a1f-a2f8-1072f855e446.png" width="750px" height="450px">
	
### 상품 INSERT
+ JpaRepository 인터페이스 save()메소드 이용해서 상품명, 가격, 재고, 상품 상세내용, 이미지 파일을 삽입합니다. 
</div>
</details>

<details>
<summary><b>상품 관리</b></summary>
<div markdown="2">
	<img src="https://user-images.githubusercontent.com/58936137/180050285-f3118855-a7df-4b9d-8dd5-f0ea1a90e2e6.png" width="750px" height="450px">
</div>
</details>

<details>
<summary><b>장바구니</b></summary>
<div markdown="2">
	<img src="https://user-images.githubusercontent.com/58936137/180050505-1fe08553-d81e-490b-a2bb-14cbf32389b0.png" width="750px" height="450px">
</div>
</details>

<details>
<summary><b>구매이력</b></summary>
<div markdown="2">
	<img src="https://user-images.githubusercontent.com/58936137/180050705-1e926b70-604b-4ddb-b2a4-a52d976b2a12.png" width="750px" height="450px">
</div>
</details>

</div>
</details>

## 👉 핵심 기능

## 👉 핵심 트러블슈팅 경험 
   



