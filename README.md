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
