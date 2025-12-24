# Project Deep Dive — Creator Portfolio (Schema + API + Consistency)

## 배경

Creator/Portfolio 기능은 “데이터 모델 + API + 캐시/정합성”이 함께 움직이는 문제입니다.
단순히 API를 추가하는 것보다,

- 스키마 설계(조회/정렬/상태)
- 운영 시나리오(숨김/비활성 등)
- Redis 인기순과 같은 캐시 정합성
  까지 고려해야 안정적인 기능이 됩니다.

## 목표

- Creator/Portfolio 도메인 도입을 위한 **스키마 설계 및 마이그레이션**
- 신규 API 제공
- 상태 변경 시 Redis 랭킹 정합성 유지

## 핵심 PRs

### 1) 스키마 도입

- Creator/Portfolio 관련 테이블 추가 및 마이그레이션

### 2) API 제공

- Creator Portfolio 신규 API 추가

### 3) Redis 인기순 정합성

- creator/portfolio 상태 변경 시 Redis 인기순 set 정리
- 도메인 모델/도메인 이벤트 기반으로 변경 포인트를 구조화

## 설계 포인트

- **상태(state) 변화가 캐시에 미치는 영향**을 명시적으로 코드에 반영
- 정합성 로직을 이벤트/도메인 모델로 분리하여
  - 변경에 강하고
  - 테스트하기 쉬운 구조를 지향

## 다음 개선 아이디어

- 인기순 캐시의 재생성 전략(재빌드 job)과 운영 도구 정리
- schema versioning 및 backward compatibility 문서화
