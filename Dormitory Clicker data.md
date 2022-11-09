## Dormitory Clicker

* 회원 기능
  
  * 로그인
    
    * Front => "/signin"
      
      ```
      POST {
          userId: "20221111",
          password: "20221111pw"
      }
      ```
    
    * Back: 성공(아이디와 비밀번호 전부 일치) / 실패
  
  * 로그아웃
    
    * 보안 기능이 따로 없어서, 프론트에서 계정정보 지우시면 될것같습니다!
  
  * 회원가입
    
    * Front => "/signup"
      
      ```
      POST {
          userId: "20221111",
          password: "20221111pw",
          userName: "금오공",
          dormitory: "오름 1동"
      }
      ```
    
    * Back: 성공 / 실패(아이디 중복 문제, 에러 발생 등)
  
  * 마이페이지 (회원정보, 예약정보)
    
    * Front
      
      ```
      POST {
          userId: "20221111"
      }
      ```
    
    * Back
      
      ```
      {
          userId: "20221111",
          password: "20221111pw",
          userName: "금오공",
          dormitory: "오름 1동",
          reservation: null or 예약정보
      }
      ```

---

* 예약 기능
  
  * 예약 버튼 클릭
    
    * Front => "/reservation"
      
      ```
      POST {
          userId: "20221111",
          dormitory: "오름 1동",
          machineNum: "W1",
          startDatetime: 2022-02-02 12:00:00,
          endDatetime: 2022-02-02 16:00:00
      }
      ```
    
    * Back: 성공 / 실패
      
      1. 예약 가능한 멤버인지 확인
      
      2. 예약 정보 db에 삽입
      
      3. canReservation 필드 0으로 수정
  
  * 예약 페이지 로드
    
    * Front => "/reservation"
      
      ```
      GET {
          dormitory: "오름 1동",
          machineNum: "W1"
      }
      ```
    
    * Back
      
      ```
      {
          startDatetime: [2022-01-01 12:00:00, ...],
          endDatetime: [2022-01-01 16:00:00, ...]
      }
      ```

---

* 메인 페이지
  
  * Front
    
    ```
    POST {
        userId: "user01"
    }
    ```
  
  * Back
    
    ```
    {
        userId: "20221111",
        dormitory: "오름 1동",
        canReservation: 1 or 0,
        W1: 1 or 2,
        W2: 1 or 2,
        ...
        D1: 1 or 2,
        D2: 1 or 2
    }
    * 1 = true / 0 = false
    ```
    
    
