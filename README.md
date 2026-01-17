
``````mermaid
flowchart TD
    %% 스타일 정의
    classDef api fill:#e3f2fd,stroke:#1565c0,stroke-width:2px,color:black;
    classDef logic fill:#fff9c4,stroke:#fbc02d,stroke-width:2px,color:black;

    Root[HODU Market 프로세스] --> Auth[회원가입/로그인]
    
    subgraph Auth_Logic [인증 프로세스]
        Auth --> A1{유저 타입}
        A1 -- 판매자 --> A2[사업자 인증 API]:::api
        A1 -- 구매자 --> A3[일반 가입]
        A2 & A3 --> A4[유효성 검사]
    end

    Auth_Logic --> Main[메인/검색]
    
    subgraph Core_Features [핵심 기능]
        Main --> S1(검색어 입력)
        S1 --> S2[Debouncing]:::logic
        S2 --> S3[추천 검색어 API]:::api
        
        Main --> P1[상품 상세]
        P1 --> P2{장바구니 담기}
        P2 --> P3[중복 체크 로직]:::logic
        P3 -- 중복X --> P4[담기 성공]
    end

    Core_Features --> Pay[결제 페이지]
    Pay --> Final[주문 완료]
```
