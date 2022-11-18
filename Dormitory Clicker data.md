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
          dormitory: "오름1"
      }
      ```
    
    * Back: 성공 / 실패(아이디 중복 문제, 에러 발생 등)
  
  * 마이페이지 (회원정보, 예약정보)
    
    * Front => "/user"
      
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
          dormitory: "오름1",
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
          dormitory: "오름1",
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
          dormitory: "오름1",
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
  
  * Front => "/dormitory"
    
    ```
    POST {
        userId: "user01"
    }
    ```
  
  * Back
    
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
    
---

* 날씨 정보 (기간설정 상의 후 수정 예정)

  * Front => "/dormitory"
    
    ```
    GET {

    }
    ```
  
  * Back
    
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
