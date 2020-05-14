# SQL-Tuning-2

# NGUYỄN THỊ HOÀI
# Ảnh của từng yêu cầu ở folder Image
# Câu số 1:
- Số lượng các node: 2
- Thông tin chi tiết của từng node: Cost, rows, width
	+ `Node 1`: cost=0.00..69.00 rows=43 width=174
	+ `Node 2`: cost=70.17..70.27 rows=43 width=174
- Node nào được chạy đầu tiên: `Node 1`
- Trình tự thực hiện các node:
	+ Đọc từng dòng từ bảng `film` và so sánh với điều kiện: `rating` = 'PG-13' AND `rental_duration` = 7 
	+ Các dòng lấy ra ở bước 1 được sắp xếp theo chiều `length` DESC
  
# Câu số 2:
- Số lượng các node: 3
- Thông tin chi tiết của từng node: Cost, rows, width
	+ `Node 1`: cost=0.00..66.50 rows=191 width=6
	+ `Node 2`: cost=67.46..67.52 rows=5 width=36
	+ `Node 3`: cost=67.58..67.59 rows=5 width=36
- Node nào được chạy đầu tiên: `Node 1`
- Trình tự thực hiện các node:
	+ Đọc từng dòng trong bảng, mỗi dòng lại tiến hành so sánh với điều kiện: `rental_duration` = 7
	+ Các dòng lấy ra ở bước 1 được tính trung bình `length` theo GROUP BY `rating`
	+ Sắp xếp các bản ghi trả về từ bước 2 theo chiều `length` DESC

# Câu số 3:
- Số lượng các node: 3
- Thông tin chi tiết của từng node: Cost, rows, width
	+ `Node 1`: cost=0.00..66.50 rows=191 width=6
	+ `Node 2`: cost=67.93..68.02 rows=2 width=36
	+ `Node 3`: cost=68.03..68.04 rows=2 width=36
- Node nào được chạy đầu tiên: `Node 1`
- Trình tự thực hiện các node:
	+ Đọc từng dòng trong bảng, mỗi dòng lại tiến hành so sánh với điều kiện: `rental_duration` = 7
  + Các dòng lấy ra ở bước 1 được tính trung bình `length` theo GROUP BY `rating` và so sánh với điều kiện: `AVG(length)` > 115
	+ Sắp xếp các bản ghi trả về từ bước 2 theo chiều `rating` DESC

# Câu số 4:
- Số lượng các node: 5
- Thông tin chi tiết của từng node: Cost, rows, width
	+ `Node 1`: cost=0.00..1.06 rows=6 width=88
	+ `Node 2`: cost=1.06..1.06 rows=6 width=88
	+ `Node 3`: cost=0.00..66.50 rows=418 width=21
	+ `Node 4`: cost=1.14..69.51 rows=418 width=103
	+ `Node 5`: cost=87.71..88.75 rows=418 width=103
- Node nào được chạy đầu tiên: `Node 1`
- Trình tự thực hiện các node: 
  + Đọc từng dòng trong bảng `language`
  + Đọc từng dòng trong bảng `film`, mỗi dòng lại tiến hành so sánh với điều kiện: `rating` = 'R' hoặc `rating` = 'PG-13'
  + Các dòng lấy ra ở bước 1 và bước 2 được join với nhau thỏa mãn điều kiện: `film.language_id` = `language.language_id`
  + Sắp xếp các bản ghi trả về từ bước 5 theo chiều `language.name` DESC

# Câu số 5:
- Số lượng các node: 6
- Thông tin chi tiết của từng node: Cost, rows, width
	+ `Node 1`: cost=0.00..1.06 rows=6 width=88
	+ `Node 2`: cost=1.06..1.06 rows=6 width=88
	+ `Node 3`: cost=0.00..66.50 rows=418 width=4
	+ `Node 4`: cost=1.14..69.51 rows=418 width=86
	+ `Node 5`: cost=71.60..71.68 rows=6 width=116
	+ `Node 6`: cost=71.75..71.77 rows=6 width=116
- Node nào được chạy đầu tiên: `Node 1`
- Trình tự thực hiện các node: 
  + Đọc từng dòng trong bảng `language`
	+ Đọc từng dòng trong bảng `film`, mỗi dòng lại tiến hành so sánh với điều kiện: `rating` = 'R' hoặc `rating` = 'PG-13'
	+ Các dòng lấy ra ở bước 1 và bước 2 được join với nhau thỏa mãn điều kiện: `film.language_id` = `language.language_id`
  + Tính toán theo GROUP BY `language.name` 
	+ Sắp xếp các bản ghi trả về từ bước 4 theo chiều `language.name` DESC

# Câu số 6:
- Số lượng các node: 8
- Thông tin chi tiết của từng node: Cost, rows, width
	+ `Node 1`: cost=0.00..4.00 rows=200 width=17
	+ `Node 2`: cost=4.00..4.00 rows=200 width=17
	+ `Node 3`: cost=0.00..64.00 rows=1000 width=4
	+ `Node 4`: cost=64.00..64.00 rows=1000 width=4
	+ `Node 5`: cost=0.00..84.62 rows=5462 width=4
  + `Node 6`: cost=76.50..175.51 rows=5462 width=6
	+ `Node 7`: cost=83.00..196.65 rows=5462 width=17
	+ `Node 8`: cost=237.62..238.90 rows=128 width=21
- Node nào được chạy đầu tiên: `Node 1`
- Trình tự thực hiện các node: 
  + Đọc từng dòng trong bảng `actor`	
  + Đọc từng dòng trong bảng `film`
  + Đọc từng dòng trong bảng `film_actor`
  + Các dòng lấy ra ở bước 3 và bước 5 được `join` với nhau thỏa mãn điều kiện: `film_actor.film_id` = `film.film_id`
  + Các dòng lấy ra ở bước 1 và bước 5 được `join` với nhau thỏa mãn điều kiện: `film_actor.actor_id` = `actor.actor_id`
  + Tính toán theo GROUP BY `actor.first_name` và `actor.last_name`
  
# Câu số 7:
- Số lượng các node: 12
- Thông tin chi tiết của từng node: Cost, rows, width
	+ `Node 1`: cost=0.00..1.16 rows=16 width=72
	+ `Node 2`: cost=1.16..1.16 rows=16 width=72
	+ `Node 3`: cost=0.28..0.53 rows=1 width=119
	+ `Node 4`: cost=0.00..4.46 rows=23 width=0
	+ `Node 5`: cost=4.46..34.36 rows=23 width=4
	+ `Node 6`: cost=34.36..34.36 rows=23 width=4
	+ `Node 7`: cost=0.00..16.00 rows=1000 width=4
	+ `Node 8`: cost=34.64..53.28 rows=23 width=8
	+ `Node 9`: cost=34.92..65.72 rows=23 width=119
	+ `Node 10`: cost=0.00..4.50 rows=1 width=17
	+ `Node 11`: cost=34.92..70.45 rows=23 width=130
	+ `Node 12`: cost=36.28..71.88 rows=23 width=196
 - Node nào được chạy đầu tiên: `Node 1`
 - Trình tự thực hiện các node: 
