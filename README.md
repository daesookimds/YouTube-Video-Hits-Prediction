## YouTube Video Hits Prediction

<img src="image/youtube_title.png" alt="subject_image" width="500" height="80">

```Let's find out what characteristics a video with a high number of views has.```

```Project Period :2018.8.16 ~```


### Objective of project

- It helps to make videos with high views by finding characteristics related to views.

***What I want to test through a project***
1. Are the number of views and elements of the video related?
2. If so, what is the correlation?
3. Can it ultimately help with youtuber or video marketing with the correlation ML find?

### Data Description

- Train data
    - train.csv : crawling data from Youtube (now 3000 row 11 columns : will be updated)

- Test data
    - Make test data by using "sklearn.model_selection.train_test_split"
    - Collect new data not included in the train.csv and test it after modeling

- Target (want to predict)
    - Average daily views
    - Because the number of views changes in real time, the daily average number of views is estimated by calculating the data collected at the time.


----------------------------------------------------------------------------------------------------------------------------------

## 유튜브 비디오 조회수 예측

```높은 조회수를 가지고 있는 동영상의 특성들을 찾아보자```

```프로젝트 기간 :2018.8.16 ~```

### 프로젝트 목적

- 프로젝트를 통해 유튜브 동영상 조회수와 상관관계가 있는 특성을 찾아 조회수 높은 동영상을 만드는 일에 도움을 준다.

***프로젝트를 통해 검증하고자 하는 것***
1. 조회수와 동영상의 요소들은 연관이 있는가?
2. 연관이 있다면, 그 상관관계는 무엇인가?
3. 궁극적으로 찾아낸 상관관계는 유튜브 크리에이터나 동영상 마케팅에 도움을 줄 수 있는가?

### 데이터 설명

- Train data
    - train.csv : 셀레니움을 활용하여 유튜브에서 크롤링한 데이터(10001개 행 13 열)
    
- Test data
    - "sklearn.model_selection.train_test_split" 을 이용하여 테스트 데이터를 만든다.
    - 모델링이 끝난 시점에 중복되지 않는 새로운 유튜브 데이터를 크롤링 하여 테스트 데이터로 이용한다.
    
- Target (예측하고자 하는 목표값)
    - 일평균 조회수
    - 조회수는 실시간으로 변화하기 때문에, 데이터를 수집한 시점을 기준으로 계산하여 일평균 조회수를 예측한다.
