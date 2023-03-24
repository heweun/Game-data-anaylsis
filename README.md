# Game-data-anaylsis
- 분석 목적 : 게임 출시를 앞두고 있는 팀원을 위한 데이터 분석
- 분석 목표 : 게임 업계 동향과 게임 출시 시 갖출 특징 파악

## 결론
1. 앱 출시량이 증가하는 것에 비해 한 앱당 다운로드 받는 횟수 감소 
2. 코로나 이전에도 게임앱 출시량 우상향    
3. 최근 3년 게임 카테고리 중 높은 순위 카테고리 Action, Casual, Arcade

#### 한 앱당 다운로드 횟수

![image](https://user-images.githubusercontent.com/109562023/227461999-6118c9ba-c849-421e-ad43-2f3ab34c2503.png) 

#### 코로나 이전 이후 게임 앱 출시량

![image](https://user-images.githubusercontent.com/109562023/227462417-a79ea279-b057-45fb-9fd4-837f5c6467da.png)

#### 인기 게임

![image](https://user-images.githubusercontent.com/109562023/227462808-fea39820-2ee7-4cb0-b02c-80a6d5566079.png)


#### 게임을 출시한다면, 다음을 특징을 갖춰 출시하는것이 좋을것으로 보인다.
1. 무료 앱
2. 전체 사용가
3. 대결에 관한 단어 포함해서 이름 짓기
4. Arcade, Casual, Puzzle, Sports의 카테고리라면 유로 앱 출시 고려
5. 인디게임이라면 2월~4월에 출시해 6월 구글 인디게임페스티벌을 목표로 하고,
    메이저게임이라면 출시 개수가 많은 달을 피하는것도 좋은 방법일 것 같다. 
    
--- 
## Lesson Learn
1. 다운로드 횟수가 누적된 데이터로 연도별로 앱 다운로드 횟수를 비교할 수 없었다.
2. 앱(게임) 시장의 추세가 아닌 사용자의 관심도를 보고자 한다면, 
 연도별 다운로드 횟수, 매출액 등의 변수들이 필요할 것으로 보인다.

---

## 분석 과정
GoogleAPI Pandas Numpy Matplotlib Notion
1. Playstore 데이터 파싱(2010.01~2022.07, 2,313,944개)
2. Pandas로 불필요한 변수, 결측치 데이터 전처리
3. Mapplotlib을 활용한 데이터 시각화

### 데이터 파싱 날짜
- 22년 7월 9일 (2010년~2022년 7월)

### 데이터 정보
| Column | Dtype | Column | Dtype |
| --- | --- | --- | --- |
| App Name | object | Minimum Android | object |
| App Id | object | Developer Id | object |
| Category | object | Developer Website | object |
| Rating | float64 | Developer Email | object |
| Rating Count | float64 | Released | object |
| Installs | object | Last Updated | object |
| Minimum Installs | float64 | Content Rating | object |
| Maximum Installs | float64 | Privacy Policy | object |
| Free | bool | Ad Supported | bool |
| Price | float64 | In App Purchases | bool |
| Currency | object | Editors Choice | bool |
| Size | object | Scraped Time | object |

### 결측치
- 개발자 웹 사이트 주소와 보안정책에 결측치가 있음
- 분석 과정에서 개발자 개인정보 columns는 제거
- 보안정책이 결측치라면 로그인이 필요없는 앱으로  column추가

### 전처리
1. 필요없는 변수 제거(Installs, Developer Id, Developer Website, Developer Email, Scraped Time)
2. 앱 이름에 결측치 있는 데이터 제거
3. Game변수 추가(대분류가 게임인 앱 True)
4. Currency가 NaN값이면 다른 변수에서도 결측치가 보여서 유의미한 데이터라고 볼 수 없다→
데이터 제거
5. Released가 결측치이면 플레이스토어 확인 결과 삭제된 앱으로 분석에 필요하지 않다고 판단→데이터제거
6. Released, Last updated 날짜 데이터로 변경
7. Released, Last updated의 연도만 가져온 Year변수 추가

### 분석 방법
- EDA를 통한 데이터 분석

1. 게임 업계 동향 파악
2. 카테고리별 출시량과 다운로드 횟수
3. 게임 카테고리별 게임명 빈도수
4. 월별 다운로드
5. 코로나 전후 비교
6. 현시점과 1년 전 비교
