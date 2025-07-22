7월 교육 내용입니다.

과목명 : 탐색적 데이터분석 입문
일정 : 7/21(월) ~ 7/24(목)



[7/21] 강의 내용


■ 중복 제거 사용
- drop_duplicaties(subset='',keep = 'first') # first는 중복중 첫번째만 남김, last 는 마지막꺼만 남김,
- dtl[dtl['주소'].duplicated(keep=False)]  Keep=False 사용하여 어떤게 중복인지 확인 가능



■ set 사용
 - set 으로 교집합을 통해 서로 다른 그룹의 같은 것을 확인 가능
 - set 은 {} 임
 - set(apt['주소'])&set(dtl['주소']) 이런식으로 활용하면 교집합으로 추려짐
 - set(apt.columns) & set(dtl.columns)

■ agg 사용해서 새로운 컬럼 값도 같이 하는법

apt.groupby(cols).agg(거래평균금액 = ('거래금액',np.mean # mean 써도 되나..?), 평당금액표준편차 = ('평당금액',np.std))



[7/22] 강의 내용

■ 쌍의 cols 을 이용한 value_counts() 사용
- 여러 쌍에서 counts 확인하기 유용( groupby + counts() 보다 편한듯)


■ 집계 사용
 - 범주형은 crosstab ## 집계 결과가 counting
 - 연속형은 pivot_table ## 집계 결과가 연속형

■ describe
 - 수치형,데이터타임 등 타입에 따라 각각 묘사 가능
 - apt.describe(include=object) : object 변수만 보며줌
 - apt.describe(include=['number']) : 수치형 모두 포함(timedelta64[ns] 포함하지만, datetime64[ns] 은 포함하지 않음)
 - apt.describe(include=['int'.'float')] : 이건 ㄹㅇ 수치형만 포함

■ 값 대체하는 법
ages = pd.Series([-1,0,2,3,15])
ages.replace([-1,0],1) : 특정 값 대체
ages.clip(lower=1,upper=5) : 1보다 작은건 1, 5보다 큰건 5로 대

■ 결측값 대체 방법
https://colab.research.google.com/drive/1xUg6ogmlV-_PvOZApx5CyfJuuyyvwzRQ?usp=sharing#scrollTo=71c63b46 (참고)
- 시간이 부족한 kaggle 에서는 시간 없으니깐 impute 사용하자

■ 결측치 확인 방법
 - apt.groupby('계약년도')['등기일자'].agg(전체건수 = 'size', 정상건수 = 'count') 와,,, count() 가 결측치 제외인지 몰랐음... 조심히 해야겠음
 - 
