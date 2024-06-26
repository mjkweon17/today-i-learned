### CSRF 공격

- CSRF(Cross-Site Request Forgery) 공격은 웹 애플리케이션 보안 취약점의 한 형태로, 공격자가 사용자의 브라우저를 속여 사용자가 의도하지 않은 액션을 웹 애플리케이션에서 수행하게 만드는 공격 기법
- 이 공격은 사용자가 해당 사이트에 로그인한 상태에서 공격자가 만든 악의적인 웹 페이지나 링크를 클릭하게 만듦으로써 이루어짐
- CSRF 공격의 핵심은 사용자가 자신의 의지와는 무관하게 공격자가 지정한 웹 요청을 보내게 만드는 것
- 예를 들어, 사용자가 은행 서비스에 로그인한 상태에서 공격자가 제공한 링크를 클릭하면, 사용자는 모르게 자신의 은행 계좌에서 공격자의 계좌로 돈을 이체하는 요청을 보낼 수 있음
- CSRF 공격을 방지하기 위한 방법으로는 토큰 기반 인증, 즉 웹 양식에 CSRF 토큰을 포함시켜 서버가 요청이 정당한지 확인할 수 있도록 하는 방법, 또는 SameSite 쿠키 속성을 사용하여 브라우저가 타 사이트의 요청에서 쿠키를 전송하지 않도록 하는 방법 등이 있음.

- CSRF 공격을 방지하기 위해 FastAPI에서 할 수 있는 것
    - CSRF 토큰 사용: 가장 일반적인 방법 중 하나는 폼이나 AJAX 요청에 CSRF 토큰을 포함시키는 것. 이 토큰은 서버에서 생성되며, 사용자 세션에 저장되어 각 요청에 포함되어야 함. 서버 측에서는 요청을 받을 때마다 이 토큰을 검증하여 요청이 유효한지 확인.
    - SameSite 쿠키 설정: 쿠키에 SameSite 속성을 설정하여, 쿠키가 같은 사이트의 요청에서만 전송되도록 함으로써 CSRF 공격을 방지할 수 있음. FastAPI에서는 응답 객체를 사용하여 쿠키를 설정할 때 SameSite 속성을 명시할 수 있음.
    - 커스텀 헤더 검증: 일부 개발자들은 커스텀 HTTP 헤더(예: X-Requested-With)를 요청에 포함시키고, 서버에서 이 헤더의 존재와 값을 검증하는 방법을 사용함. 이 방법은 단순하지만, 모든 클라이언트가 이 헤더를 지원하지는 않을 수 있음.
    - Double Submit Cookie: CSRF 토큰을 쿠키와 요청 페이로드(예: 폼 데이터) 양쪽에 제출하고, 서버에서 이 두 값을 비교하는 방식. 이 방법은 토큰을 사용자 세션에 저장할 필요가 없어 세션리스(stateless) 애플리케이션에 적합할 수 있음.
    - 사용자 인터랙션 요구: 중요한 작업(예: 비밀번호 변경, 계정 삭제 등)에 대해 추가적인 사용자 인증(예: 비밀번호 재입력, CAPTCHA 확인)을 요구함으로써, 공격자가 사용자의 의도하지 않은 행동을 유발하는 것을 방지할 수 있음.
    - 보안 라이브러리 활용: Starlette(이는 FastAPI의 핵심에 있음)이나 다른 FastAPI 호환 보안 라이브러리에서 제공하는 보안 기능을 활용할 수 있음. 이러한 라이브러리는 CSRF 방지를 위한 토큰 생성 및 검증 메커니즘을 제공할 수 있음.

### SameSite 쿠키 속성
- SameSite 쿠키 속성은 웹 브라우저가 쿠키를 언제 전송할지 제어하는 방법을 제공하는 쿠키의 보안 기능
- 이 속성을 통해 웹사이트는 CSRF(Cross-Site Request Forgery) 공격을 방지하는 데 도움을 받을 수 있음
- SameSite 속성은 세 가지 주요 값을 가질 수 있으며, 각각의 값은 브라우저가 쿠키를 전송하는 방식을 다르게 지정함
    1. Strict: 이 값이 설정된 쿠키는 오직 원본 도메인에서만 전송됨. 예를 들어, 사용자가 직접 웹사이트를 방문했을 때만 쿠키가 전송됨. 다른 사이트에서 링크를 통해 해당 사이트로 이동할 경우, 쿠키는 전송되지 않음. 이는 사용자의 개인정보 보호에 가장 엄격하지만, 사용자 경험을 저하시킬 수 있음.
    2.Lax: 이는 SameSite 속성의 기본 설정이며, 대부분의 쿠키에 적합한 보안 수준을 제공함. 'Lax' 모드에서는 쿠키가 타 사이트에서 발생한 GET 요청(예: 링크 클릭을 통해 사이트에 접근하는 경우)에 대해서는 전송되지만, POST 요청(예: 타 사이트의 양식에서 데이터를 제출하는 경우)에 대해서는 전송되지 않음. 이 설정은 사용자 경험을 해치지 않으면서도 많은 CSRF 공격을 방지할 수 잇음.
    3. None: 쿠키가 모든 요청에 대해 전송되도록 허용함. 즉, 타 사이트에서 오는 요청에 대해서도 쿠키를 전송할 수 있음. 이 옵션을 사용할 때는 반드시 쿠키를 `Secure`로 설정해야 함. 즉, 쿠키가 오직 HTTPS를 통해서만 전송되도록 해야 함. 'None' 설정은 특정 타입의 크로스-사이트 요청이 필요한 경우에 유용할 수 있지만, CSRF 공격에 취약할 수 있으므로 주의가 필요함.