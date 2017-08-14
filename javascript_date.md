# JAVASCRIPT - DATE

날짜와 시간을 위한 메소드를 제공하는 BUILT-IN객체

>내부적으로 DATE객체는 숫자값을 갖는다.

## 1. DATE CONSTRUCTOR
DATE 생성자를 사용해 날짜와 시간을 가지는 인스턴스를 생성한다.  
>생성된 인스턴스는 기본적으로 오늘 날짜와 시간을 가진다.

날짜와 시간을 가지는 DATE객체를 생성하는 방법
```javascript
new Date()
new Date(milliseconds)
new Date(dateString)
new Date(year, month[, day, hour, minute, second, millisecond])
```

`Date()생성자 함수를 new 연산자를 붙이지 않아 생성자로 사용하지 않으면 Date객체를 반환하지 않고 결과값을 문자열로 반환한다.`

> 매개변수에 따라 Date 생성자의 동작은 달라진다.

### 1. new Date()
매개변수가 없는 경우 현재 날짜와 시간을 가지는 인스턴스를 반환한다.

### 2. new Date(milliseconds)
매개변수에 밀리초를 전달하면 : 1970년 1월 1일 00:00(UTC)기점으로 전달된 밀리초만큼 경과한 날짜와 시간을 가지는 인스턴스를 반환한다.

>86400000ms : 1day

```
1s = 1,000ms
1m = 60s * 1,000ms = 60,000ms
1h = 60m * 60,000ms = 3,600,000ms
1d = 24h * 3,600,000ms = 86,400,000ms
```
- KST : GMT에 9시간을 더한 시간

### 3. new Date(dateString)
매개변수에 날짜와 시간을 나타내는 문자열을 전달하면 지정된 날짜와 시간을 가지는 인스턴스를 반환

> 이때 함수에 전달된 문자열은 parse()메소드에 의해 인식 가능한 형식이어야 한다.

```javascript
var d = new Date('2017/08/08/20:00:00');
console.log(d); // Tue Aug 08 2017 20:00:00 GMT+0900 (KST)
```

### 4. new Date(year, month[,day, hour, minute, second, millisecond])
매개변수에 년,월,일,시,분,초,밀리초를 의미하는 숫자를 전달하면 지정된 날짜와 시간을 가지는 인스턴스를 반환한다.
>이때 년,월을 반드시 지정하여야 한다. 지정하지 않은 옵션 정보는 0또는 1 으로 초기화된다.

인수목록
- year : 1900년 이후의 년
- month : 월을 나타내는 0~11까지의 정수
- day : 1~31까지의 정수
- hour : 0~23까지의 정수
- minute : 0~59까지의 정수
- second : 0~59까지의 정수
- millisecond : 0~999까지의 정수

## 2. Date Method

### 1. Date.now()
현재까지의 시간을 밀리초로 반환한다.

### 2. Date.parse()
매개변수로 전달된 지정시간 까지의 밀리초를 숫자로 반환한다.
>Date(dateString)의 인수와 동일한 형식까지

`현재 로컬로 가지고 있는 시간시스템을 적용해 계산한다.`
- utc를 기준으로 하고 싶다면
```javascript
var d = Date.parse('Jan 2, 1970 00:00:00 UTC'); // UTC
console.log(d); // 86400000
```
### 3. Date.UTC()
매개변수로 전달된 지정시간까지의 밀리초를 숫자로 반환한다.

```javascript
var d = Date.UTC(1970, 0, 2);
console.log(d); // 86400000

var d = Date.UTC('1970/1/2');
console.log(d); // NaN
```
> utc로 인식된다.
### 4. Date.prototype.getFullYear()
해당 연도를 나타내는 4자리 숫자를 반환한다.

### 5. Date.prototype.setFullYear()
해당 연도를 나타내느 4자리 숫자를 설정한다. 연도 이외 월,일도 설정할 수 있다.

```javascript
dateObj.setFullYear(yearValue[, monthValue[, dayValue]])
```

### 6. Date.prototype.getMonth()
해당 월을 나타내는  0~11의 정수를 반환한다.

>1월은 0, 12월은 11이다.

### 7. Date.prototype.setMonth()
해당 월을 나타내는 0~11 정수를 설정한다.
>월 이외 일도 설정할 수 있다.
```javascript
dateObj.setMonth(monthValue[, dayValue])
```

### 8. Date.prototype.getDate()
해당 날짜를 나타내는 정수를 반환한다.

### 9. Date.prototype.setDate()
해당 날짜를 나타내는 정수를 설정한다.

### 10. Date.prototype.getDay()
해당 요일을 나타내는 정수를 반환한다.

`반환값`
- 일요일 : 0
- 월요일 : 1
- 화요일 : 2 
- 수요일 : 3
- 목요일 : 4
- 금요일 : 5
- 토요일 : 6

### 11. Date.prototype.getHours()
해당 시간을 나타내는 정수를 반환

### 12. Date.prototype.setHours()
해당 시간을 나타내는 정수를 설정

> 시간 이외 분, 초, 밀리초도 설정할 수 있다.

```javascript
dateObj.setHours(hoursValue[, minutesValue[, secondsValue[, msValue]]])
```

### 13. Date.prototype.getMinutes()
해당 분을 나타내는 정수를 반환한다.

### 14. Date.prototype.setMinutes()
해당 분을 나타내는 정수를 설정한다.
> 분 이외 초, 밀리초도 설정할 수 있다.
```javascript
dateObj.setMinutes(minutesValue[, secondsValue[, msValue]])
```

### 15. Date.prototype.getSeconds()
해당 초를 나타내는 정수를 반환한다.

### 16. Date.prototype.setSeconds()
해당 초를 나타내는 정수를 설정한다.

> 초 이외 밀리초도 설정할 수 있다.

```javascript
dateObj.setSeconds(secondsValue[, msValue])
```

### 17. Date.prototype.getMilliseconds()
해당 밀리초(0~999)를 나타내는 정수를 반환

### 18. Date.prototype.setMilliseconds()
해당 밀리초를 나타내는 정수를 설정한다.

### 19. Date.prototype.getTime()
UTC를 기점으로 현재시간까지의 밀리초를 반환한다.

### 20. Date.prototype.setTime()
UTC를 기점으로 현재시간까지의 밀리초를 설정한다.
```javascript
dateObj.setTime(timeValue)
```

### 21. Date.prototype.getTimezoneOffset()
UTC와 지정로케일 시간과의 차이를 분단위로 반환

> KST : UTC에 9시간을 더한시간 . UTC = KST -9H이다.

### 22. Date.prototype.toDateString()
사람이 읽을 수 있는 형식의 문자열로 날짜를 반환

### 23. Date.prototype.toTimeString()
사람이 읽을 수 있는 형식의 문자열로 시간을 반환

## 3. Date Example
```javascript
(function printNow() {
  var today = new Date();

  var dayNames = ['(일요일)', '(월요일)', '(화요일)', '(수요일)', '(목요일)', '(금요일)', '(토요일)'];
  var day = dayNames[today.getDay()];

  var year   = today.getFullYear(),
      month  = today.getMonth() + 1,
      date   = today.getDate(),
      hour   = today.getHours(),
      minute = today.getMinutes(),
      second = today.getSeconds();
      ampm   = hour >= 12 ? 'PM' : 'AM';

  // 12시간제로 변경
  hour = hour % 12;
  hour = hour ? hour : 12; // the hour '0' should be '12'

  // 10미만인 분과 초를 2자리로 변경
  minute = minute < 10 ? '0' + minute : minute;
  second = second < 10 ? '0' + second : second;

  var now =  year + '년 ' + month + '월 ' + date + '일 ' + day + ' ' + hour + ':' + minute + ':' + second + ' ' + ampm;

  console.log(now);
  setTimeout(printNow, 1000);
}());
```