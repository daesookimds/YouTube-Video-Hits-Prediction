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

### Data Preprocessing

- upload_date : divide into year, month, day. (upload_date_year, upload_date_month, upload_date_day)
- crawl_date : divide into year, month, day. (crawl_date_year, crawl_date_month, crawl_date_day)
- uploaded_days : the number of days since the movie was posted before it was collected.
- views : number of hits at the time of collection / uploaded_days
- dislike : change object types into numeric types.
- like : change object types into numeric types.
- comments : the number of comments, change object types into numeric types.
- subscribers : the number of subscribers, change object types into numeric types.
- play_time : total video playback time
- title_length : the length of title
- tag_count : the number of tag
- same_count : The same number of words between the title and tag.
- title_cosine_similarity : the cosine similarity between title and tag.
- comment_cosine_similarity : the cosine similarity between top_comment and tag.(top_comment is the most popular comment.)
- category : one-hot encode to ['title', 'game', 'science', 'education', 'style', 'news', 'animal', 'social', 'sports',
                       'entertainment', 'journey', 'movie', 'music', 'people', 'automobile', 'comic', 'program']
                       
                       
### Feature Selection and Correlation.

- At first, using 33 columns to train lightGBM becasue to look at feature importance of views prediction
      
       ['comments', 'dislike', 'like',
       'play_time', 'subscribers',
       'upload_date_year', 'upload_date_month', 'upload_date_day',
       'crawl_date_year', 'crawl_date_month', 'crawl_date_day',
       'uploaded_days', 'title_length', 'tag_count', 'same_count',
       'title_cosine_similarity', 'game', 'science', 'education', 'style',
       'news', 'animal', 'social', 'sports', 'entertainment', 'journey',
       'movie', 'music', 'people', 'automobile', 'comic', 'program', 'comment_cosine_similarity']
       
  that case: high importance features are like, dislike, (the number of)comments, subscribers, uploaded_days to predict views
  
 
- Second, remove multicollinearity by using VIF(variance_inflation_factor)
  then, using 8 columns to train Statsmodels.OLS because to look at linear correlations
       
        ['like', 'dislike', 'comments', 'play_time', 'subscribers', 'title_length', 'title_cosine_similarity',
        'comment_cosine_similarity']
        
 
- Last, remove features that are out of trust in p-value 0.05
  then, using 4 columns to train Statsmodels.OLS because to look at linear correlations
       
        ['like', 'dislike', 'title_length', 'comment_cosine_similarity']
        
        
    'like', 'title_length', 'comment_cosine_similarity' is a positive correlation with the number of hits.
    'dislike' is a negative correlation with the number of hits.
                       

### Result

- As a result of limited data, this is not best answer.

- If you want to predict the number of views, focus on the like, dislike, (the number of)comments, (the number of)subscribers, uploaded_days.

- If you want to increase the number of views, get 'LIKE' and write a comment similar to the tag first.

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

### 데이터 전처리

- upload_date : 년, 월, 일로 나누어준다. (upload_date_year, upload_date_month, upload_date_day)
- crawl_date : 년, 월, 일로 나누어준다. (crawl_date_year, crawl_date_month, crawl_date_day)
- uploaded_days : 동영상이 게시된 시점부터 크롤링된 시점까지의 일 수
- views : 크롤링된 시점의 총 조회수 / 동영상이 게시된 시점부터 크롤링된 시점까지의 일 수 = 일평균 조회수
- dislike : 문자형으로 되어있는 데이터를 숫자로 바꾸어준다.
- like : 문자형으로 되어있는 데이터를 숫자로 바꾸어준다.
- comments : 댓글 수, 문자형으로 되어있는 데이터를 숫자로 바꾸어준다.
- subscribers : 구독자 수, 문자형으로 되어있는 데이터를 숫자로 바꾸어준다.
- play_time : 동영상 총 재생시간
- title_length : 제목의 길이
- tag_count : 태그의 수
- same_count : 제목과 태그 사이에 같은 단어 수
- title_cosine_similarity : 제목과 태그 사이에 코사인 유사도
- comment_cosine_similarity : 제목과 제일 인기있는 댓글 사이에 코사인 유사도(top_comment is the most popular comment.)
- category : 원-핫 인코딩 ['title', 'game', 'science', 'education', 'style', 'news', 'animal', 'social', 'sports',
                       'entertainment', 'journey', 'movie', 'music', 'people', 'automobile', 'comic', 'program']


### 특성 선택 및 상관관계 보기

- 처음에, 조회수를 예측할 때 중요한 특성들을 추려보기 위해 33개의 열을 가지고 lightGBM모델로 학습 시켜본다.
      
       ['comments', 'dislike', 'like',
       'play_time', 'subscribers',
       'upload_date_year', 'upload_date_month', 'upload_date_day',
       'crawl_date_year', 'crawl_date_month', 'crawl_date_day',
       'uploaded_days', 'title_length', 'tag_count', 'same_count',
       'title_cosine_similarity', 'game', 'science', 'education', 'style',
       'news', 'animal', 'social', 'sports', 'entertainment', 'journey',
       'movie', 'music', 'people', 'automobile', 'comic', 'program', 'comment_cosine_similarity']
       
       
  이 경우: 높은 중요도를 나타내는 특성은 dislike, (the number of)comments, subscribers, uploaded_days 이다.
  
 
- 그 다음으로, VIF(variance_inflation_factor)을 이용하여 다중공선성을 없애준다.
  그 후, 8개의 열로 Statsmodels.OLS을 사용하여 선형관계를 파악해본다.

       ['like', 'dislike', 'comments', 'play_time', 'subscribers', 'title_length', 'title_cosine_similarity',
        'comment_cosine_similarity']
        
 
- 마지막으로, p-value 0.05가 넘는 경우의 열을 제거한다.
  그 후, 4개의 열을 가지고 Statsmodels.OLS 로 학습하여 선형관계를 파악한다.
 
        ['like', 'dislike', 'title_length', 'comment_cosine_similarity']
      
        
     'like', 'title_length', 'comment_cosine_similarity' 는 조회수와 양의 상관관계이다.
     'dislike' 는 조회수와 음의 상관관계이다.
        
### 결과

- 제한된 10000개의 데이터를 사용하였기 때문에 정답이 아니다.

- 조회수를 예측하고 싶다면 '좋아요', '싫어요' 수와 댓글수, 구독자수, 업로드된 후 지난 일 수를 살펴보면 된다.

- 조회수가 향상되도록 유도하고 싶다면 '좋아요'를 누르도록 유도하고 첫 댓글로 태그와 비슷한 댓글 설명을 쓰면 좋다. 
