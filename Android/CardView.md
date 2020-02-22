### 이슈
1. 5.0 이하 단말에서 배경색이 검은색으로 나타나는 현상

### 원인
1. `android:background` 속성으로 배경색 변경 시, 5.0 이하에서는 적용되지 않음

### 대책
1. `app:cardBackgroundColor` 속성을 사용하도록 변경
   - 공식 레퍼런스 문서에서 `app:cardBackgroundColor` 를 사용하는 것으로 가이드 되어 있음
