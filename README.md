# Tài liệu mô tả API Lbasense HUST

##Lấy danh sách id và tên region

- Tham số truyên lên (kiểu POST)

| Parameter   | Type            |		Description               |
|--------------| ------------------|-----------------------------|
| type   | String             | RegionNames          |
| user       | String	            | student-hust    |
| pass       | String         | 123456a@          |

- Dữ liệu lấy về
  + Mã region
  + Tên region

Ví dụ: 
```
{"1":"HUST1","2":"HUST2","3":"HUST3","4":"HUST4"}
```

##Lấy số lượng người hiện tại đang ở một region

- Tham số truyên lên (kiểu POST)

| Parameter   | Type            |		Description               |
|--------------| ------------------|-----------------------------|
| type   | String             | CurrentVisitorValuePerRegion          |
| user       | String	            | student-hust    |
| pass       | String         | 123456a@          |

- Dữ liệu lấy về

| Parameter   | Type            |		Description               |
|--------------| ------------------|-----------------------------|
| date  | String             | Thời điểm dữ liệu trả về          |
| sapInformation  | Array             | Mảng dữ liệu visitor thời điểm hiện tại         |
| regionID  | Integer             | Mã region         |
| numVisitors  | Integer             | Tổng số visitor hiện tại ở region         |
| changeRate  | Integer             | Tham số thể hiện mức độ thay đổi của số visitor hiện tại và số visitor của 1 phút trước |


Ví dụ:
```
{"date":"2016-10-07T08:48:00","sapInformation":[{"regionID":1,"changeRate":0,"numVisitors":133},{"regionID":2,"changeRate":0,"numVisitors":242},{"regionID":3,"changeRate":0,"numVisitors":0},{"regionID":4,"changeRate":0,"numVisitors":0}]}
```
##Lấy số liệu thống kê theo khoảng thời gian
###Cách 1

- Tham số truyên lên (kiểu POST)

| Parameter   | Type            |		Description               |
|--------------| ------------------|-----------------------------|
| type   | String             | StatsSummary          |
| user       | String	            | student-hust    |
| pass       | String         | 123456a@          |
| region       | Integer         | id region lấy ở trên          |
| startTime       | String         | Thời điểm bắt đầu cần lấy số liệu. Ví dụ: 2016-09-12T00:00:00          |
| endTime       | String         | Thời điểm cuối cần lấy số liệu. Ví dụ: 2016-09-12T00:00:00          |
| resolution       | String         | days/hours          |

- Dữ liệu lấy về

| Parameter   | Type            |		Description               |
|--------------| ------------------|-----------------------------|
| summaryStats   | Array             | Mảng dữ liệu trả về          |
| date   | String             | Thời điểm lấy dữ liệu         |
| numVisitors   | Integer             | Tổng số lượng visitor         |
| numReturningVisitors   | Integer             | Số lượng người tới và quay trở lại region trong khoảng 4 tháng gần đây.|
| avgDuration   | Integer             | Khảng thời gian trung bình tính theo giây mà mọi người đứng tại region         |



Ví dụ dữ liệu lấy theo resolution là hours:
```
{"summaryStats":[{"date":"2016-10-06T00:00:00","numVisitors":276,"numReturningVisitors":174,"avgDuration":5620},{"date":"2016-10-06T01:00:00","numVisitors":172,"numReturningVisitors":117,"avgDuration":7469}]}
```

Ví dụ dữ liệu lấy theo resolution là days:
```
{"summaryStats":[{"date":"2016-10-02","numVisitors":21403,"numReturningVisitors":11234,"avgDuration":629},{"date":"2016-10-03","numVisitors":29687,"numReturningVisitors":20472,"avgDuration":914},{"date":"2016-10-04","numVisitors":32856,"numReturningVisitors":21900,"avgDuration":867},{"date":"2016-10-05","numVisitors":30663,"numReturningVisitors":21214,"avgDuration":878}]}
```

###Cách 2

- Tham số truyên lên (kiểu POST)

| Parameter   | Type            |		Description               |
|--------------| ------------------|-----------------------------|
| type   | String             | VisitorCounts          |
| user       | String	            | student-hust    |
| pass       | String         | 123456a@          |
| region       | Integer         | id region lấy ở trên          |
| startTime       | String         | Thời điểm bắt đầu cần lấy số liệu. Ví dụ: 2016-09-12T00:00:00          |
| endTime       | String         | Thời điểm cuối cần lấy số liệu. Ví dụ: 2016-09-12T00:00:00          |
| resolution       | String         | days/hours          |

- Dữ liệu lấy về

| Parameter   | Type            |		Description               |
|--------------| ------------------|-----------------------------|
| date   | Array             | Danh giờ hoặc ngày     |
| visitorCounts   | Array             | Số lượng người ởregion tương ứng với mảng date bên trên    |

Ví dụ dữ liệu lấy theo resolution là hours:

```
{"dates":["2016-10-02T00:00:00","2016-10-02T01:00:00"],"visitorCounts":[256,171]}
```

Ví dụ dữ liệu lấy theo resolution là days:

```
{"dates":["2016-10-02T00:00:00","2016-10-03T00:00:00","2016-10-04T00:00:00","2016-10-05T00:00:00"],"visitorCounts":[21403,29687,32856,30663]}
```

##Lấy số liệu thống kê thời gian các visitor ở lại region

- Tham số truyên lên (kiểu POST)

| Parameter   | Type            |		Description               |
|--------------| ------------------|-----------------------------|
| type   | String             | VisitDurations          |
| user       | String	            | student-hust    |
| pass       | String         | 123456a@          |
| region       | Integer         | id region lấy ở trên          |
| startTime       | String         | Thời điểm bắt đầu cần lấy số liệu. Ví dụ: 2016-10-01          |
| endTime       | String         | Thời điểm cuối cần lấy số liệu. Ví dụ: 2016-10-04          |

- Dữ liệu lấy về

| Parameter   | Type            |		Description               |
|--------------| ------------------|-----------------------------|
| visitDurations   | Array             |Danh sách các ngày lấy số liệu và thông tin của từng ngày |
| date   | String             | Ngày lấy số liệu    |
| from1To5Minutes   | Integer             | Số lượng người đứng tại region trong khoảng thời gian từ 1 tới 5 phút    |
| from5To10Minutes   | Integer             | Số lượng người đứng tại region trong khoảng thời gian từ 5 tới 10 phút    |

Ví dụ

```
{"visitDurations":[{"date":"2016-10-01","under1Minute":11658,"from1To5Minutes":1199,"from5To10Minutes":487,"from10To20Minutes":575,"from20To40Minutes":607,"from40To60Minutes":241,"from60To90Minutes":216,"from90To120Minutes":150,"from2To3Hours":135,"from3To4Hours":67,"from4To6Hours":64,"over6Hours":69},{"date":"2016-10-02","under1Minute":14576,"from1To5Minutes":1502,"from5To10Minutes":630,"from10To20Minutes":796,"from20To40Minutes":775,"from40To60Minutes":244,"from60To90Minutes":179,"from90To120Minutes":116,"from2To3Hours":126,"from3To4Hours":63,"from4To6Hours":76,"over6Hours":85},{"date":"2016-10-03","under1Minute":17996,"from1To5Minutes":2727,"from5To10Minutes":1248,"from10To20Minutes":1491,"from20To40Minutes":1600,"from40To60Minutes":634,"from60To90Minutes":568,"from90To120Minutes":395,"from2To3Hours":418,"from3To4Hours":154,"from4To6Hours":149,"over6Hours":142}]}
```
