---
layout: post
title: Zipline KRX Trading Calendar 문제
tags: ["zipline", "python"]
---

### 시스템 환경
* python version : 3.5 (32bits)
* zipline version : 1.3.0

zipline 샘플 구동시 KOSPI 개장일부터 일봉을 받아 돌려보니 index error 발생. #TradingCanlendar 문제로 보이며 #KRX 에 맞는 #Canlendar 를 만들어야 함

```python
class TFSExchangeCalendar(TradingCalendar):
    """
    An exchange calendar for trading assets 24/7.
    Open Time: 12AM, UTC
    Close Time: 11:59PM, UTC
    """ 

    @property
    def name(self):
        """
        The name of the exchange, which Zipline will look for
        when we run our algorithm and pass TFS to
        the --trading-calendar CLI flag.
        """
        return "TFS"


    @property
    def tz(self):
        """
        The timezone in which we'll be running our algorithm.
        """
        return timezone("UTC")
 

    @property
    def open_time(self):
        """
        The time in which our exchange will open each day.
        """
        return time(0, 0)
 

    @property
    def close_time(self):
        """
        The time in which our exchange will close each day.
        """
        return time(23, 59)
 

    @lazyval
    def day(self):
        """
        The days on which our exchange will be open.
        """
        weekmask = "Mon Tue Wed Thu Fri Sat Sun"
        
        return CustomBusinessDay(
            weekmask=weekmask
        )
    
    #출처 : http://www.zipline.io/trading-calendars.html#building-a-custom-trading-calendar (2019.01.14)
```

1. open_time() 에서 잘못된 부분  
  - 메소드 명 : open_times()
  - 리턴 데이터형 : [(None, time object)]
2. close_time() 에서 잘못된 부분
  - 메소드 명 : close_times()
  - 리턴 데이터형 : [(None, time object)]
3. weekmask 는 @property로 정의된 메소드 존재 (선언할 필요 없음). 즉, day함수 자체 선언 불필요하며 부모함수에서 참조하는 property method들만 override하면 됨

### 참고사이트
* [영업일과 휴일 - 한국거래소](https://financedata.github.io/posts/pandas-market-days-krx.html)
* [Time Series / Date functionality — pandas 0.23.4 documentation](https://pandas.pydata.org/pandas-docs/stable/timeseries.html)
* [How to make a only Sunday(30-10-2016) as a Trading Day · Issue #2337 · quantopian/zipline](https://github.com/quantopian/zipline/issues/2337)
* [pandas.tseries.offsets.CustomBusinessDay — pandas 0.24.0rc1+13.ge2bf1ff4 documentation](https://pandas-docs.github.io/pandas-docs-travis/api/generated/pandas.tseries.offsets.CustomBusinessDay.html)
