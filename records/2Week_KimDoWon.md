## Title: [2Week] 김도원
<br/>

### 미션 요구사항 분석 & 체크리스트

---
#### 필수미션: 호감표시 시 실행하는 예외처리 Case 3가지 구현

- [x] Case 4
  - [x] 동일한 호감상대에게 동일한 사유로는 호감표시 불가
  - [x] rq.historyBack 사용

- [x] Case 5
  - [x] 모든 인스타회원은 10명까지만 호감표시 가능
  - [x] 사유 상관없이 10명
  - [x] rq.historyBack 사용

- [x] Case 6
  -  [x] Case 4 발생 시 기존의 사유와 다른 사유로 호감을 표시하는 경우에는 성공으로 처리
  -  [x] 새 호감상대 등록이 아니라 기존 호감표시를 수정해야 함
  -  [x] resultCode = "S-2"
  -  [x] msg = "OOO에 대한 호감사유를 외모에서 성격으로 변경합니다."

<br/>

### 1주차 미션 요약

---

**[접근 방법]**

구현 순서: Case 4 → Case 6 → Case 5

Case 4
- likeablePersonService에 `canActorLike` 메서드 구현
- likeablePersonRepository의 `findByFromInstaMemberIdAndToInstaMember_username 사용
  - 현재 로그인한 인스타 멤버(FromInstaMemberId)의 id와 새로 입력한 username(ToInstaMember_username), 두 개의 데이터와 일치하는 likeablePerson 객체 찾기
- likeablePerson 객체가 null일 경우, 동일한 호감표시가 존재하지 않으므로 S-1 리턴 
- `likeablePerson.getAttractiveTypeCode() == attractiveTypeCode`
  - 이 객체의 AttractiveTypeCode와 새로 입력한 attractiveTypeCode가 일치하면 F-3 리턴
  - 일치하지 않으면 Case 6 

Case 6
- 안전성을 위해 `@Setter`를 사용하는 대신 업데이트가 필요한 값만을 따로 변경하는 메서드 `updateAttractiveType`를 구현
- 값의 변경이 발생하므로 `canActorLike` 메서드에 `@transactional` 붙이기

Case 5
- likeablePersonService에 `checkMax` 메서드 따로 구현

<br/>

**[특이사항]**
- 10개의 호감표시가 존재할 때 `checkMax` 메서드가 `canActorLike` 메서드보다 먼저 실행될 경우, Case 6은 새로운 호감상대를 추가하는 것이 아님에도 실행되지 않는다. 그래서 반드시 `checkMax` 메서드가 `canActorLike` 메서드보다 뒤에 위치해야 함

<br/>

**[Refactoring]**
- 선택미션 네이버 로그인 구현하기
- stream을 활용하여 코드 가독성 높이기