## Title: [1Week] 김도원

### 미션 요구사항 분석 & 체크리스트

---
- [x] 호감상대 삭제 기능 구현
    - [x] url의 `[likeablePerson.id](http://likeablePerson.id)` 와 일치하는 데이터를 DB에서 삭제
    - [x] 삭제 권한 체크 (본인이 등록한 호감상대만 삭제 가능)
    - [x] 삭제 후 다시 호감목록 페이지로 이동 (rq.redirectWithMsg 함수 사용)
    - [x] 삭제 버튼 style 적용

- [ ] 테스트케이스 작성
    - [ ] 호감상대 삭제


### 1주차 미션 요약

---

**[접근 방법]**

- `호감상대 삭제 = DB에서 LikeablePerson 테이블의 row 하나를 삭제하는 것` 에 중점을 두고 구현하였습니다.
- 미션 진행하기 전 실습했던 <점프 투 스프링부트> 책과 gramgram 프로젝트를 참고하였습니다.

- 목표: 삭제권한 체크 후 삭제처리 & 확인창 보여주기


1. 호감상대 삭제 기능 구현
- @GetMapping 어노테이션을 사용하여 LikeablePersonController의 delete() 메서드를 list.html에서 요청된 URL과 매핑
- 요청된 URL에서 `[likeablePerson.id](http://likeablePerson.id)` 는 Controller의 매개변수로 받을 때 likeablePerson. 없이 id만 작성해야 함
    - 그렇지 않으면 오류발생
- 매개변수 id와 일치하는 likeablePerson 객체 가져오기
    - 객체를 쉽게 가져오기 위해 `likeablePersonService에 getLikeablePerson`() 메서드 구현
- rq의 getMember() 메서드를 사용하여 현재 로그인한 Member의 객체를 가져와서 likeablePerson 객체 안의 FromInstaMember의 id와 일치하는지 확인하기
- `rq.redirectWithMsg()`를 활용하여 메세지 출력하고 호감목록으로 이동하기


2. 테스트케이스 작성
- MockMvc 클래스와 resultActions 클래스 등을 다루는 것이 어려워 미완료


**[특이사항]**

- test에 .param 입력하는 것이 어려움


**[Refactoring]**
- 삭제 완료 후 뜨는 확인창 표시시간 줄이기