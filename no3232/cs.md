# prepare_frontend_interview

## Computer Science

## 목차

- [CORS 🔥](#CORS)

  - CORS가 뭔가요?
  - CORS를 겪고 직접 해결해 본 경험이 있으면 말해주세요

## CORS

### CORS가 뭔가요?

CORS(Cross-Origin Resource Sharing)

웹에서 다른 도메인 혹은 포트 등에 대한 접근을 허용하는 정책.
보통 다른 도메인에서 리소스를 요청 할 때 발생한다.

정확히는 다른 오리진에서 리소스를 요청 할 때 발생한다.

> 오리진 vs 리소스?
>
> 오리진은 프로토콜(http, https), 호스트(www.example.com), 포트(443)를 포함한 전체 주소를 의미한다.
>
> 예: https://www.example.com:443
>
> 리소스는 오리진 이후의 경로와 파일을 의미한다.
> 예: /path/to/resource.html
>
> 전체 URL 예시: https://www.example.com:443/path/to/resource.html

브라우저에서만 나타나기 때문에 서버와 서버간의 통신에서는 발생하지 않는다. 따라서 외부 API를 사용할 때 프론트에서 직접 사용하는 것이 아닌 서버에서 처리하는 이유가 이것 때문일 수 있다.

앱에서는 CORS 정책이 직접적으로 적용되지 않지만, 앱 내 웹뷰를 사용하거나
네이티브 HTTP 요청을 할 때 서버 측에서 CORS 설정이 필요할 수 있다.

CORS 통신을 하게 되면 네트워크 탭에서 OPTIONS 요청이 추가로 발생한다.

이 요청은 실제 데이터를 전송하는 요청이 아니고 실제 요청 전에 서버에 안전하게 요청을 보낼 수 있는지 확인하는 **"프리플라이트"** 요청이다.

보통 프론트에서는 헤더에 `WithCredentials: true`와 함께 리퀘스트를 보내고, 백엔드에서는 `Access-Control-Request-Method`와 `Access-Control-Request-Headers`를 포함하여 리스폰스를 보낸다.

### CORS를 겪고 직접 해결해 본 경험이 있으면 말해주세요

개발환경과 실제 배포환경에서 해결하는 방식으로 나누어보자.

1. 개발환경

   package.json에서 프록시 설정을 변경하여 해결할 수 있다.

   ```json
   {
     "name": "your-project-name",
     "version": "1.0.0",
     "private": true,
     "dependencies": {
       // ... 다른 의존성들 ...
     },
     "scripts": {
       // ... 스크립트들 ...
     },
     "proxy": "http://api.example.com"
   }
   ```

   위와 같이 설정하면 api요청이 프록시를 통해서 전달된다. 하지만 위 방법은 개발 환경에서만 동작을 하기 때문에 실 배포에서는 사용할 수 없는 방법.

2. 실제 배포환경

   1. 서버에서 허용해주는 방법
   2. 프록시 서버를 사용하는 방법

   위 두가지 방법으로 나뉜다.

   1. 서버에서 허용해주는 방법

      서버에서 허용해주는 방법은 서버에서 허용할 오리진을 명시해주는 방법이다.
      Nest에서는 다음과 같이 서버에서 허용할 수 있다.

      ```typescript
      // main.ts
      import { NestFactory } from "@nestjs/core";
      import { AppModule } from "./app.module";

      app.enableCors({
        origin: ["http://localhost:3000"],
      });

      bootstrap();
      ```

   2. 프록시 서버를 사용하는 방법

      이 방법은 서버와 서버간에는 CORS가 발생하지 않기 때문에 중간에 프록시서버를 두고 이를 통해 요청을 넣는 방법이다.

      Nginx를 사용하여 프록시 서버를 구축할 수 있다. 또는 헤로쿠에서도 프록시 서버를 구축할 수 있다. Next.js에서도 서버 api를 사용할 수 있기 때문에 프록시 역할을 하는 서버를 구축할 수 있다.
