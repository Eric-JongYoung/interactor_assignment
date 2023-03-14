# Interactor Assignment 1st

# ✅ 구성

## 🧩 AutoFlow 폴더
- AutoFlow config.json 파일 첨부

## 🧩 svelte-basic-training 폴더 
- AutoFlow 에서 보내준 DB를 Svelte의 Ajax 통신을 통하여 데이터 반환.
(fetch와 {#await ..} 적용)
- JavaScript 를 이용하여 페이징 처리 및 이전, 다음 페이지 기능 구현.


# Interactor Assignment 2nd

## 🧩 AutoFlow 폴더
- GET http://localhost:8000/board/:id 요청 시 MySQL의
training 스키마(데이터베이스)에서 board 테이블의 id 값이 :id 파라미터에 해당하는 데이터
를 하나 반환하는 Server Endpoint를 생성

## 🧩 svelte-basic-training 폴더 
- 기존 board 페이지의 리스트에서 제목을 클릭하면 /board/:id 페이지로 이동되도록 수
정
- /board/:id 페이지에서는 제목, 등록일자, 내용이 표시되도록 기능 구현
- 이전 게시물, 다음 게시물로 이동하는 버튼 추가 기능 구현