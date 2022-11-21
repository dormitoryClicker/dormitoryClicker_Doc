Dormitory Clicker

- 회원 기능
  
  - 로그인
    
    - Front => "/signin"
      
      ```
      POST {
          userId: "20221111",
          password: "20221111pw"
      }
      ```
      
    - Back
      
      - 아이디/비밀번호 일치
        
        ```
        "success"
        ```
        
      - 아이디/비밀번호 불일치
        
        ```
        "failed"
        ```
        
  - 로그아웃
    
    - 보안 기능이 따로 없어서, 프론트에서 계정정보 지우시면 될것같습니다!
  - 회원가입
    
    - Front => "/signup"
      
      ```
      POST {
          userId: "20221111",
          password: "20221111pw",
          userName: "금오공",
          dormitory: "오름 1동"
      }
      ```
      
    - Back
      
      - 회원가입 성공
        
        ```
        "success"
        ```
        
      - 중복된 아이디로 실패
        
        ```
        "Id exists"
        ```
        
  - 마이페이지 (회원정보, 예약정보)
    
    - Front
      
      ```
      POST {
          userId: "20221111"
      }
      ```
      
    - Back
      
      - 성공
        
        ```
        {
            userId: "20221111",
            password: "20221111pw",
            userName: "금오공",
            dormitory: "오름 1동",
            reservation: null or 예약정보
        }
        ```
        
      - 아이디 없어서 실패: 404
        
        ```
        "Not found userId with ${userId}"
        ```
        
      - 서버 문제로 실패: 500
        
        ```
        "Server Unavailable"
        ```
        

---

- 예약 기능
  
  - 예약 버튼 클릭
    
    - Front => "/reservation"
      
      ```
      POST {
          userId: "20221111",
          dormitory: "오름 1동",
          machineNum: "W1",
          startDatetime: 2022-02-02 12:00:00,
          endDatetime: 2022-02-02 16:00:00
      }
      ```
      
    - Back: 성공 / 실패
      
      1. 예약 가능한 멤버가 아니면
        
        ```
        "already reservation"
        ```
        
      2. 기기 확인이 안되면
        
        ```
        "There's no machine"
        ```
        
      3. 예약 정보 db에 삽입 + canReservation 필드 0으로 수정 성공
        
        ```
        "success"
        ```
        
  - 예약 페이지 로드
    
    - Front => "/reservation"
      
      ```
      GET {
          dormitory: "오름 1동",
          machineNum: "W1"
      }
      ```
      
    - Back
      
      - 성공
        
        ```
        {
            startDatetime: [2022-01-01 12:00:00, ...],
            endDatetime: [2022-01-01 16:00:00, ...]
        }
        ```
        
      - 기기 확인 안돼서 실패
        
        ```
        "There's no machine"
        ```
        

---

- 메인 페이지
  
  - Front => "/dormitory"
    
    ```
    POST {
        userId: "user01"
    }
    ```
    
    - Back
      
      - 성공
        
        ```
        [
          {
              "machineNum": "W1",
              "state": 0
          },
          {
              "machineNum": "W2",
              "state": 1
          },
          {
              "machineNum": "W3",
              "state": 1
          },
          {
              "machineNum": "W4",
              "state": 1
          },
          {
              "machineNum": "D1",
              "state": 1
          },
          {
              "machineNum": "D2",
              "state": 1
          }
        ]
        * 1 = true (현재 사용 가능) / 0 = false (현재 사용 중)
        ```
        
      
      - 기숙사 존재하지 않음: 404
        
        ```
        not found dormitory with ${기숙사 이름}
        ```
        
      - 서버 문제로 실패: 500
        
        ```
        "Server Unavailable"
        ```
        

---

- 날씨 정보 (기간설정 상의 후 수정 예정)
  
  - Front => "/"
    
    ```
    GET {
    
    }
    ```
    
  - Back
    
    ```
    [
    {
        "date": "2022-11-18 09:00:00",
        "weather": "Clear"
    },
    {
        "date": "2022-11-18 12:00:00",
        "weather": "Clear"
    },
    {
        "date": "2022-11-18 15:00:00",
        "weather": "Clear"
    },
    {
        "date": "2022-11-18 18:00:00",
        "weather": "Clouds"
    },
    {
        "date": "2022-11-18 21:00:00",
        "weather": "Clouds"
    },
    {
        "date": "2022-11-19 00:00:00",
        "weather": "Clouds"
    },
    {
        "date": "2022-11-19 03:00:00",
        "weather": "Clouds"
    },
    {
        "date": "2022-11-19 06:00:00",
        "weather": "Clouds"
    },
    {
        "date": "2022-11-19 09:00:00",
        "weather": "Clouds"
    },
    {
        "date": "2022-11-19 12:00:00",
        "weather": "Clouds"
    },
    {
        "date": "2022-11-19 15:00:00",
        "weather": "Clouds"
    },
    {
        "date": "2022-11-19 18:00:00",
        "weather": "Clouds"
    },
    {
        "date": "2022-11-19 21:00:00",
        "weather": "Clouds"
    },
    
    ...,
    
    {
        "date": "2022-11-23 00:00:00",
        "weather": "Clouds"
    },
    {
        "date": "2022-11-23 03:00:00",
        "weather": "Clouds"
    },
    {
        "date": "2022-11-23 06:00:00",
        "weather": "Clouds"
    }
    ]
    ```
