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
