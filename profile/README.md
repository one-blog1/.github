# One Blog

**회원이 블로그를 만들고, 다른 회원과 함께 운영하는 블로그 커뮤니티**

혼자 쓰는 블로그를 넘어, 관심사가 같은 사람들이 한 블로그에 모여 같이 글을 쓰고 운영합니다. 메인에서 가입하고 블로그를 만들거나 참여하며, 글은 각자의 블로그에서 씁니다.

![Java](https://img.shields.io/badge/Java_21-ED8B00?logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot_4.1-6DB33F?logo=springboot&logoColor=white)
![Spring Security](https://img.shields.io/badge/Spring_Security-6DB33F?logo=springsecurity&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL_8.4-4479A1?logo=mysql&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?logo=githubactions&logoColor=white)

## 주요 기능

| 영역 | 기능 |
|---|---|
| 회원 | 이메일 인증 가입, 소셜 로그인(카카오·네이버·구글), 로그인 유지, 계정 찾기, 내 정보·설정(알림, 공개 범위, 차단, 화면 테마) |
| 블로그 | 블로그 만들기(공개·일부 공개·비공개), 참여 신청·승인, 블로그장·부블로그장·멤버 역할, 멤버 관리, 위임·폐쇄 |
| 글 | 마크다운 에디터, 사진 첨부, 유튜브·치지직·SOOP 영상 재생, 카테고리·태그, 최신순·인기순, 조회수, SNS 공유 미리보기 |
| 소통 | 댓글·답글, 좋아요, 회원 팔로우, 블로그 구독, 프로필, 알림 |
| 메인 | 내 블로그 새 글, 메인 피드, 통합 검색, 큰 사진 배너(인기 글·새 블로그·인기 블로그·광고), 공지사항 |
| 운영 | 관리자 화면(회원·글·댓글·신고 처리, 공지, 배너, 통계, 처리 기록), 블로그별 제재·블랙리스트·신고 |

## 기술과 구조

- **서버**: Spring Boot 4.1 · Java 21 · Spring Security 7 · JPA(Hibernate 7) · Flyway · MySQL 8.4
- **화면**: 정적 HTML + JavaScript. 서버 하나가 화면과 API를 함께 내보내는 모놀리스 구조
- **보안**: JWT + HttpOnly 쿠키 로그인, CSRF 토큰, 보안 헤더(CSP 등), 비밀번호 bcrypt, 글 본문 HTML 필터링, 요청 제한
- **배포**: GitHub Actions에서 테스트 → Docker 이미지 → 서버에 무중단 배포(nginx 앞에 블루·그린 두 컨테이너를 번갈아 씀). 새 버전이 상태 확인을 통과하지 못하면 이전 버전을 그대로 유지

```
main에 버전을 올려 합침 → CI(전체 테스트, 실행 확인) → Docker 이미지 → 서버 블루/그린 교체 → 버전 태그
```

## 개발 방식

- **명세부터**: 기능마다 [GitHub Spec Kit](https://github.com/github/spec-kit)으로 명세 → 계획 → 작업 → 구현 순서로 진행하고, 요구사항 번호를 근거로 남깁니다.
- **DB 설계**: ERD를 먼저 고치고, 테이블은 Flyway 마이그레이션으로 추가합니다.
- **브랜치**: `feature/*` → `develop` → (버전을 올릴 때) `main`. 운영 버그는 `hotfix/*`로 고쳐 main과 develop에 함께 반영합니다.
- **버전**: 배포할 때마다 0.01씩 올리고, 버전마다 릴리즈 노트를 남깁니다.

## 저장소

| 저장소 | 내용 |
|---|---|
| [one_blog](https://github.com/one-blog1/one_blog) | 서비스 소스 코드와 배포 설정 |
| [one-blog_docs](https://github.com/one-blog1/one-blog_docs) | 요구사항 분석서, 기능 명세(Spec Kit), 결정 기록, 릴리즈 노트 |
