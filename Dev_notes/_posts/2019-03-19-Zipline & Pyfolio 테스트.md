---
layout: post
title: Zipline & Pyfolio 테스트
tags: ["zipline", "python"]
---

### 시스템 환경
* python version : 3.5 (32bits)
* zipline version : 1.3.0
* google colab

### zipline 
KODEX200(069500) 기초자산의 데이터를 Pandas.Panel 객체로 구성

```
  <class 'pandas.core.panel.Panel'>
  Dimensions: 1 (items) x 3943 (major_axis) x 5 (minor_axis)
  Items axis: 069500 to 069500
  Major_axis axis: 2002-10-14 00:00:00 to 2018-09-13 00:00:00
  Minor_axis axis: open to volume
```

트레이딩 알고리즘은 13,26일 이평선을 기준으로 상향돌파시 매수, 하향돌파시 전량매도 하는 기본전략 사용하였습니다.
(수수료, 슬리피지는 기본값 사용)

```python
  try:    
      start = pd.Timestamp('2013-01-01', tz='utc')
      end = pd.Timestamp('2017-12-31', tz='utc')

      #run algo
      perf = zipline.run_algorithm(start=start, end=end,
                                  initialize=initialize, 
                                  handle_data=handle_data,
                                  capital_base=100000,
                                  data_frequency='daily', 
                                  data=symbol_panel,
                                  trading_calendar=KRXExchangeCalendar()
                                  )
  except Exception:
      logging.exception('Exception occurs')
  else:
      perf.to_pickle('logs/perf.pickle')
```

### Pyfolio

pyfolio.create_full_tear_sheet() 호출 결과

> Annual return 2.8%  
> Cumulative returns 14.4%  
> Annual volatility 5.0%  
> Sharpe ratio 0.57  
> Calmar ratio 0.27  
> Stability 0.50  
> Max drawdown -10.5%  
> Omega ratio 1.18  
> Sortino ratio 0.88  
> Skew 1.34  
> Kurtosis 31.21  
> Tail ratio 1.22  
> Daily value at risk -0.6%  
> Gross leverage 0.56  
> Daily turnover 3.0%  
> Alpha 0.01  
> Beta 0.22

* {{ post.dir }}
* {{ post.path }}
* {{ post.url }}
* {{ post.catogory }}
* {{ post.categories }}
* {{ post.categories[0] }}

![pyfolio_20190319]({{post.path}}/images/pyfolio_20190319.png)
![pyfolio_20190319_dir]({{ post.dir }}/images/pyfolio_20190319.png)
