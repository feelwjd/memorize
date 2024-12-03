SAP XSUAA(XSUAA: XSUAA(Identity Authentication and Authorization)은 SAP Cloud Platform의 주요 서비스 중 하나로, OAuth 2.0 및 OpenID Connect(OIDC)를 기반으로 사용자 인증 및 권한 부여를 관리하는 서비스입니다.
이 서비스는 애플리케이션과 마이크로서비스가 안전하게 인증 및 권한 부여를 수행할 수 있도록 지원합니다. 
XSUAA는 특히 SAP BTP(Business Technology Platform)에서 애플리케이션을 구축하거나 확장할 때 중요한 역할을 합니다.

# 작동 방식
XSUAA는 OAuth 2.0 및 OpenID Connect 프로토콜을 지원하며, 여러 인증 흐름을 통해 애플리케이션과 사용자 간의 안전한 인증을 관리합니다. 이를 통해 애플리케이션은 사용자를 인증하고 보호된 리소스에 대한 접근을 제어할 수 있습니다. XSUAA의 주요 기능은 다음과 같습니다:

#### **OAuth 2.0 및 OpenID Connect 지원**

- **OAuth 2.0**: 자원을 소유한 사용자가 자원 소유자로서 자원 접근 권한을 제3자 애플리케이션에 위임할 수 있는 인증 프로토콜입니다.
- **OpenID Connect(OIDC)**: OAuth 2.0을 기반으로 한 인증 레이어로, 사용자 인증 정보를 추가적으로 제공합니다.

#### **주요 OAuth 2.0 인증 흐름 지원**

XSUAA는 여러 OAuth 2.0 인증 흐름을 지원합니다. 각 인증 흐름은 다양한 시나리오에 맞게 설계되어 있습니다:

1. **Authorization Code Grant**:
    
    - 가장 일반적인 인증 흐름으로, 서버 사이드 애플리케이션에서 주로 사용됩니다.
    - 사용자 에이전트(예: 브라우저)를 통해 인증 서버로 리디렉션하고, 사용자가 인증을 완료한 후 Authorization Code를 애플리케이션으로 전달합니다.
    - 애플리케이션은 Authorization Code를 사용하여 인증 서버에서 액세스 토큰을 요청하고, 보호된 리소스에 접근합니다.
2. **Implicit Grant**:
    
    - 클라이언트 쪽 애플리케이션(예: JavaScript SPA)에서 주로 사용되며, 액세스 토큰이 직접 클라이언트로 전달됩니다.
    - 보안상의 이유로 권장되지 않으며, 현재는 거의 사용되지 않습니다.
3. **Resource Owner Password Credentials Grant**:
    
    - 사용자의 자격 증명(사용자 이름 및 비밀번호)을 직접 사용하여 액세스 토큰을 요청하는 방식입니다.
    - 사용자와 신뢰 관계가 있는 애플리케이션에서 주로 사용되며, 보안상의 이유로 제한적으로만 사용됩니다.
4. **Client Credentials Grant**:
    
    - 애플리케이션 자체가 리소스 소유자로 인증될 때 사용됩니다. 주로 서버 간 통신이나 서비스 간 통신에서 사용됩니다.
    - 액세스 토큰은 애플리케이션 클라이언트 자격 증명을 사용하여 요청됩니다.

#### **Access Token 및 Refresh Token**

- **Access Token**: 인증 서버가 발급하는 JWT(JSON Web Token) 형식의 토큰으로, 보호된 리소스에 대한 접근 권한을 나타냅니다. Access Token은 유효 기간이 제한되어 있습니다.
- **Refresh Token**: Access Token이 만료된 경우 새 Access Token을 발급받기 위해 사용됩니다. Refresh Token은 일반적으로 더 긴 유효 기간을 가지며, 주기적으로 새로고침하여 사용합니다.


# 사용 이유 및 이점
XSUAA는 SAP BTP의 애플리케이션 및 마이크로서비스 환경에서 인증 및 권한 부여를 위한 필수 서비스로, 여러 이점이 있습니다:

#### **보안 강화**

- **중앙 집중식 인증 관리**: XSUAA는 모든 애플리케이션과 마이크로서비스에 대한 중앙 집중식 인증 및 권한 부여를 제공합니다. 이를 통해 보안 정책을 통합적으로 관리할 수 있습니다.
- **OAuth 2.0 및 OIDC 표준 준수**: XSUAA는 OAuth 2.0 및 OpenID Connect 표준을 준수하여 다양한 인증 흐름과 보안 시나리오를 지원합니다.

#### **유연성**

- **다양한 인증 흐름 지원**: XSUAA는 여러 OAuth 2.0 인증 흐름을 지원하므로, 애플리케이션의 요구에 따라 적절한 흐름을 선택할 수 있습니다.
- **다중 테넌시 지원**: XSUAA는 여러 테넌트를 지원하여, 하나의 XSUAA 인스턴스에서 여러 고객 또는 애플리케이션을 관리할 수 있습니다.

#### **간편한 통합**

- **SAP BTP와의 긴밀한 통합**: XSUAA는 SAP BTP의 네이티브 서비스로, 다른 SAP BTP 서비스와 쉽게 통합할 수 있습니다. 예를 들어, SAP Cloud Foundry 애플리케이션과 쉽게 통합됩니다.
- **애플리케이션 간 Single Sign-On(SSO)**: XSUAA를 통해 여러 애플리케이션 간에 SSO를 구현할 수 있어, 사용자 경험을 개선하고 보안을 강화할 수 있습니다.


# 사용 방법
XSUAA를 사용하려면 다음 단계에 따라 설정합니다:

#### **1. XSUAA 인스턴스 생성**

1. **SAP BTP Cockpit에 로그인**: SAP BTP Cockpit에 로그인하고, XSUAA 서비스를 사용하고자 하는 서브어카운트로 이동합니다.
2. **서비스 인스턴스 생성**: "Services" > "Instances and Subscriptions"로 이동하여 XSUAA 서비스를 검색하고 인스턴스를 생성합니다.
3. **서비스 플랜 선택**: 필요한 권한과 기능에 맞는 서비스 플랜을 선택합니다.

#### **2. XSUAA 보안 설정**

1. **OAuth2 클라이언트 구성**: XSUAA 인스턴스 내에서 애플리케이션을 위한 OAuth2 클라이언트를 구성합니다. 이 과정에서는 클라이언트 ID, 클라이언트 시크릿, 권한(Scopes), 리디렉션 URI 등을 설정합니다.
2. **트러스트 구성**: 신뢰할 수 있는 인증 제공자(IdP)를 구성하여, 다양한 IdP와의 통합을 설정할 수 있습니다.

#### **3. Spring Boot 애플리케이션과의 통합**

1. **Spring Security 설정**: `application.properties` 파일에서 Spring Security와 OAuth2 클라이언트를 설정합니다.
2. **보안 필터 체인 구성**: Spring Security의 `SecurityFilterChain`을 사용하여 인증 및 권한 부여 흐름을 설정합니다.


```
curl --location 'https://cesco-dev-8g9e0txu-dev-ccw-approuter.cfapps.ap12.hana.ondemand.com/com-srv/account/Departments' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsImprdSI6Imh0dHBzOi8vY2VzY28tZGV2LThnOWUwdHh1LmF1dGhlbnRpY2F0aW9uLmFwMTIuaGFuYS5vbmRlbWFuZC5jb20vdG9rZW5fa2V5cyIsImtpZCI6ImRlZmF1bHQtand0LWtleS0yMTQwYjg1YjYwIiwidHlwIjoiSldUIiwiamlkIjogIjI0R0l1djh6RnZ4NVNZaDRvb1ptemFOMml0RDNCdWlBZm1LdmtWZVpGbFE9In0.eyJqdGkiOiJlYzViYjM2NDY3YTU0ODUyYmE3YjkzYzY2NzIzNTdkOSIsImV4dF9hdHRyIjp7ImVuaGFuY2VyIjoiWFNVQUEiLCJzdWJhY2NvdW50aWQiOiJmZGZjZTJiNy05NGMzLTRlMmQtOWE5Yi1lZWM2NTVmZWRlZDIiLCJ6ZG4iOiJjZXNjby1kZXYtOGc5ZTB0eHUiLCJvaWRjSXNzdWVyIjoiaHR0cHM6Ly9hY2NvdW50cy5zYXAuY29tIn0sInVzZXJfdXVpZCI6ImUwZGFlNDJhLTllNzQtNDJjNi05ZjVmLWE4YWY1Y2YzYzU4ZCIsInhzLnVzZXIuYXR0cmlidXRlcyI6e30sInhzLnN5c3RlbS5hdHRyaWJ1dGVzIjp7InhzLnJvbGVjb2xsZWN0aW9ucyI6WyJBTExfUk9MRVMiXX0sImdpdmVuX25hbWUiOiJKZW9uZ1BpbCIsImZhbWlseV9uYW1lIjoiTWluIiwic3ViIjoiMDc1OTBlNGQtZTMyMC00NGQxLTk0YzAtZjBhMjgzMzQ2NTQ3Iiwic2NvcGUiOlsib3BlbmlkIiwidWFhLnVzZXIiXSwiY2xpZW50X2lkIjoic2ItY29tLWNlc2NvLWRldi04ZzllMHR4dS1ERVYhdDQ3MDQiLCJjaWQiOiJzYi1jb20tY2VzY28tZGV2LThnOWUwdHh1LURFViF0NDcwNCIsImF6cCI6InNiLWNvbS1jZXNjby1kZXYtOGc5ZTB0eHUtREVWIXQ0NzA0IiwiZ3JhbnRfdHlwZSI6InBhc3N3b3JkIiwidXNlcl9pZCI6IjA3NTkwZTRkLWUzMjAtNDRkMS05NGMwLWYwYTI4MzM0NjU0NyIsIm9yaWdpbiI6InNhcC5kZWZhdWx0IiwidXNlcl9uYW1lIjoiZmVlbHdqZEBnbWFpbC5jb20iLCJlbWFpbCI6ImZlZWx3amRAZ21haWwuY29tIiwiYXV0aF90aW1lIjoxNzI1ODQ3NjI2LCJyZXZfc2lnIjoiNzQzY2Q1OWEiLCJpYXQiOjE3MjU4NDc2MjcsImV4cCI6MTcyNTg0OTQyNywiaXNzIjoiaHR0cHM6Ly9jZXNjby1kZXYtOGc5ZTB0eHUuYXV0aGVudGljYXRpb24uYXAxMi5oYW5hLm9uZGVtYW5kLmNvbS9vYXV0aC90b2tlbiIsInppZCI6ImZkZmNlMmI3LTk0YzMtNGUyZC05YTliLWVlYzY1NWZlZGVkMiIsImF1ZCI6WyJ1YWEiLCJvcGVuaWQiLCJzYi1jb20tY2VzY28tZGV2LThnOWUwdHh1LURFViF0NDcwNCJdfQ.k2ZuTx_kF4pg5FAbnkPribRR1FMbwUkBCZAhtmVvN2ZejzIJ78SmDOKMpBBD-KbOsdkm-GLxgh1MPEga3CBJ-XwlzGVbpU5BbfEn80gFn0lKFxDfHQrEokrGrcZDgbg15yNSlsMlAVdX3JqSp8qnyzLIPlm6CQdg2semvi4QD0wv2QGzTVVDriTm_pcU2dXXQCdkCBku_r3qeUVn7iXDRdIMnujtJ2kQ71P5EvRho7eBlVAJ8kar8bLb1f698fNI8U84clKSBb_JLONKGgnGaYQwwd9c2FXRDnm09iQVvrxG4cVbjXpqTAsu7xWgge2Uhgldw-RPjiXu4MfXoyiUZw' \
--data ''

```


```
curl 'https://cesco-dev-8g9e0txu-dev-ccw-approuter.cfapps.ap12.hana.ondemand.com/com-srv/account/Departments' \
  -H 'accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7' \
  -H 'accept-language: ko,en-US;q=0.9,en;q=0.8' \
  -H 'cache-control: max-age=0' \
  -H 'cookie: slo_regular_domains_eu1_services_services=H4sIAAAAAAAAADMxrZw%2Bw1RN6iub15%2BFXhf%2B2cUxfjud6qKdVjN5UuflhQoAwZYGcCAAAAA%3D; JTENANTSESSIONID_services=zfQTv%2BhgjTFqJJBH4q213BklRQikkddBa8yfzW9V48E%3D; __VCAP_ID__=24bba46d-bca3-4486-5247-9887; JSESSIONID=s%3APC8YClux3xwfR4MGtmxZdVHMJowaV7b9.IYfeGwLUkVpUtTdDNJyHbR66Vz7Eoe8A1TuFVFtAuX0' \
  -H 'dnt: 1' \
  -H 'priority: u=0, i' \
  -H 'referer: https://cesco-dev-8g9e0txu-dev-ccw-approuter.cfapps.ap12.hana.ondemand.com/com-srv/account/Departments' \
  -H 'sec-ch-ua: "Not;A=Brand";v="24", "Chromium";v="128"' \
  -H 'sec-ch-ua-mobile: ?1' \
  -H 'sec-ch-ua-platform: "Android"' \
  -H 'sec-fetch-dest: document' \
  -H 'sec-fetch-mode: navigate' \
  -H 'sec-fetch-site: same-origin' \
  -H 'sec-fetch-user: ?1' \
  -H 'upgrade-insecure-requests: 1' \
  -H 'user-agent: Mozilla/5.0 (Linux; Android 8.0.0; SM-G955U Build/R16NW) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.0.0 Mobile Safari/537.36'
```




https://cesco-dev-8g9e0txu-dev-srs-approuter.cfapps.ap12.hana.ondemand.com/svm-srv/$api-docs/odata/v4/auto-staffing

https://cesco-dev-8g9e0txu-dev-srs-approuter.cfapps.ap12.hana.ondemand.com/svm-srv/odata/v4/auto-staffing