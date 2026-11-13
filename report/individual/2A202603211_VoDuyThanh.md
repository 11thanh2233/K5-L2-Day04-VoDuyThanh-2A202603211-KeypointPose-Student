# Báo cáo cá nhân — 2A202603211-VoDuyThanh

Đổi tên file theo quy tắc `MSSV_HoTen.md`. Ví dụ: `20241234_NguyenVanAn.md`.

Dữ liệu: 12 ảnh người COCO val2017 (Lin et al., 2014) và 8 ảnh chân dung Wikimedia Commons, chỉ dùng trong lớp.

## 0. Thông tin học viên

- Họ tên: Võ Duy Thành
- MSSV: 2A202603211
- Email: 26ai.thanhvd@vinuni.edu.vn
- Link repository: https://github.com/11thanh2233/K5-L2-Day04-VoDuyThanh-2A202603211-KeypointPose-Student.git
- Phiên bản CVAT (Help → About): 2.74.1
- Máy: hệ điều hành Windows 10 · RAM 8 GB · chạy CVAT chế độ đầy đủ
- Bộ ảnh (`src/exports/assignment.json` do `lab.py setup` tạo): có
- Giờ bắt đầu: 20h30
- Giờ kết thúc: 22h00

## 1. Kiểm tra label (CP0)

| Label    | Kiểu     | Số điểm | Tên điểm đúng bảng của lab? | Đúng thứ tự? | Số cạnh |
| -------- | -------- | ------: | --------------------------- | ------------ | ------: |
| `person` | skeleton |      17 | Có                          | Có           |      19 |
| `face`   | skeleton |      13 | Có                          | Có           |      13 |

Mẫu `person` dựng theo người quay mặt về camera (các điểm `left_*` nằm bên phải khung mẫu)? Có

Cách đổi cờ `occluded` / `outside` cho **một điểm** trên phiên bản CVAT này (một câu):
Trên thanh Objects bên phải để hiện danh sách điểm, bấm biểu tượng `occluded` / `outside` trên dòng của đúng điểm đó (hoặc rê chuột lên điểm trên canvas và nhấn `Q` cho occluded, `O` cho outside).

## 2. Số lượng đã gán và thời gian (CP1, CP2)

| Nhóm ảnh   | Số ảnh | Số skeleton đã gán | Số người dưới 60 px (không gán) | Số poster / gương / màn hình bỏ qua | Thời gian (phút) |
| ---------- | -----: | -----------------: | ------------------------------: | ----------------------------------: | ---------------: |
| `easy`     |      5 |                  5 |                               0 |                                   0 |               30 |
| `occluded` |      3 |                  3 |                               0 |                                   0 |               20 |
| `back`     |      2 |                  2 |                               0 |                                   0 |               10 |
| `small`    |      1 |                  1 |                               0 |                                   0 |                5 |
| `crowd`    |      1 |                  1 |                               0 |                                   0 |                5 |
| `faces`    |      8 |                  8 |                               0 |                                   0 |               30 |

- Số ảnh người đã xong ở mốc phút 105: 10 / 10
- Thời gian thực tế (phút): CP1 80' · CP2 35' · CP3 25'
- Ảnh tốn thời gian nhất là ảnh nào, vì sao? 000000007281.jpg do 2 người cần gán skeleton là da đen và ảnh mờ nên có nhiều chi tiết khá khó để gán

...

## 3. Bảng ca khó (CP1, CP2)

Mỗi điểm bạn phân vân một dòng, nhất là phân vân giữa `v = 1` và `v = 0`, hoặc không chắc hướng người.

| Ảnh              | Người / mặt | Điểm                        | Cờ đã chọn | Phân vân giữa       | Lý do chọn                                                                                         |
| ---------------- | ----------- | --------------------------- | ---------: | ------------------- | -------------------------------------------------------------------------------------------------- |
| 000000007281.jpg | người       | left_ear                    |   occluded | occluded và outside | vì người đội nón che đi một phần cũng như da đen và ảnh mờ nên sẽ khó xác định phần tai            |
| 000000188804.jpg | người       | left_ankle của người áo đen |    outside | outside và occluded | vì người mặc áo đen ngay kế viền ảnh sẽ rất khó để đoán vị trí khuỷu tay, không đảm bảo được v = 1 |
| face_99874.jpg   | mặt         | vị trí phần mắt             |    outside | occluded và outside | do người đeo kính râm có phản xạ nên không thể phán đoán vị trí của mắt, v sẽ gần bằng 0 hơn       |

## 4. Bảng tự review (CP3)

Đi từ ảnh cuối về ảnh đầu. 5 ảnh người (ít nhất 2 ảnh `back` hoặc `crowd`) và 3 ảnh mặt. Ít nhất 8 dòng, kể cả dòng `ok`. Ghi lỗi trước, sửa sau.

Mã lỗi dùng đúng một trong: `lr_swap`, `vis_flag`, `position`, `missing`, `extra`, `ok`.

| Ảnh              | Người / mặt | Điểm | Mã lỗi   | Ghi chú                                                                      | Đã sửa?  |
| ---------------- | ----------- | ---- | -------- | ---------------------------------------------------------------------------- | -------- |
| 000000522889.jpg | người       | 34   | lr_swap  | crowd, cặp knee nằm ngược phía so với các cặp còn lại do chân bắt chéo thật. | chưa sửa |
| 000000431988.jpg | người       | 29   | vis_flag | crowd, left_wrist nằm ở ngoài ảnh nên set thành outside.                     | đã sửa   |
| 000000343057.jpg | người       | 15   | lr_swap  | cặp knee nằm ngược phía so với các cặp còn lại do chân bắt chéo thật.        | chưa sửa |
| 000000311300.jpg | người       | 22   | lr_swap  | crowd, cặp knee nằm ngược phía so với các cặp còn lại do chân bắt chéo thật. | chưa sửa |
| 000000188804.jpg | người       | 22   | lr_swap  | crowd, cặp knee nằm ngược phía so với các cặp còn lại do chân bắt chéo thật. | chưa sửa |
| face_99874.jpg   | mặt         | 5    | vis_flag | occluded hoặc outside do băng mắt che hoàn toàn, không đoán được vị trí mắt  | chưa sửa |
| face_504911.jpg  | mặt         | 13   | ok       | không tìm thấy lỗi.                                                          | chưa sửa |
| face_560526.jpg  | mặt         | 5    | vis_flag | occluded hoặc outside do kính râm che khuất hoàn toàn mắt.                   | chưa sửa |


Tổng hợp số lỗi theo mã:

| `lr_swap` | `vis_flag` | `position` | `missing` | `extra` | `ok` |
| --------: | ---------: | ---------: | --------: | ------: | ---: |
|         4 |          3 |          0 |         0 |       0 |    1 |

Điểm còn phân vân giữa `v = 1` và `v = 0` (ghi cả hai lựa chọn và lý do chọn): ở hình face_99874 và face_560526, lựa chọn ở mắt người có thể là v = 1 (occluded) nhưng do băng mắt/kính râm che khuất hoàn toàn, không thể dự đoán hoặc làm dự đoán vị trí mắt trở nên cực kỳ không chắc chắn nên v = 0 (outside) trở thành 1 lựa chọn an toàn hơn.
``
...

## 5. Kiểm file xuất và kết quả tự kiểm (CP4)

Tự kiểm tay trong file JSON:

| File                     | Người / mặt kiểm (ảnh, thứ tự)         | Số phần tử `keypoints` | Điểm `outside` ra `v = 0`, `occluded` ra `v = 1`?    | `num_keypoints` khớp?                        |
| ------------------------ | -------------------------------------- | ---------------------: | ---------------------------------------------------- | -------------------------------------------- |
| `VoDuyThanh_persons.zip` | 000000056651.jpg, người #1             |                     51 | Có                                                   | Có: 16 = 11 điểm `v = 2` + 5 điểm `v = 1`    |
| `VoDuyThanh_persons.zip` | 000000188804.jpg, người #2 (quay lưng) |                     51 | Có                                                   | Có: 11 = 8 điểm `v = 2` + 3 điểm `v = 1`     |
| `VoDuyThanh_faces.zip`   | face_99874.jpg, mặt #1                 |                     39 | 8 điểm mắt ra `v = 0`; mặt này không có điểm `v = 1` | Có: 5 = 5 điểm `v = 2` (mũi và 4 điểm miệng) |

Sau khi xuất, CVAT ghi `occluded` thành `v = 1` và `outside` thành `v = 0`. Tọa độ của điểm `outside` trong file là `0, 0` hay tọa độ cũ? Tọa độ cũ.

Hai job đã chuyển sang completed trên CVAT? Có.

Dán phần **TÓM TẮT** in ra từ `src/check_submission.py`:

```text
- File person: VoDuyThanh_persons.zip
  Số ảnh: 12 · số skeleton `person`: 20 · mỗi annotation 51 số
  Skeleton theo ảnh: 000000007281=2, 000000056651=2, 000000103970=1, 000000156069=1, 000000162046=1, 000000188804=2, 000000201702=1, 000000311300=2, 000000343057=1, 000000431988=2, 000000516902=2, 000000522889=3
  Cờ v: v=2 215 (63%) · v=1 48 (14%) · v=0 77 (23%)
  num_keypoints trung bình: 13.2
- File face: VoDuyThanh_faces.zip
  Số ảnh: 8 · số skeleton `face`: 8 · mỗi annotation 39 số
  Skeleton theo ảnh: face_137371=1, face_185015=1, face_496353=1, face_504911=1, face_560526=1, face_575921=1, face_85624=1, face_99874=1
  Cờ v: v=2 88 (85%) · v=1 0 (0%) · v=0 16 (15%)
  num_keypoints trung bình: 11.0
- Ghi chú: 93 điểm v = 0 vẫn mang tọa độ cũ (CVAT 2.x xuất như vậy; chuẩn COCO ghi 0, 0). Không phải lỗi: điểm v = 0 bị bỏ qua khi huấn luyện và khi chấm.
- Số [LỖI]: 0 · số [CẢNH BÁO]: 5
Kết quả: ĐẠT (đọc lại từng cảnh báo ở trên)
```

Các `[CẢNH BÁO]` còn giữ nguyên và lý do: Giữ 4 cảnh báo lr_swap do người trong hình bắt chéo chân thật.

...

## 6. Ảnh chụp màn hình

1. Label `person` trong label constructor (đủ 17 điểm có tên):

   ![Label person](images/1_label_person.png)

2. Một người quay lưng đã gán, cờ đã đặt:

   ![Người quay lưng](images/2_nguoi_quay_lung.png)

3. Một khuôn mặt đã gán 13 điểm, phóng to vùng mắt:

   ![Khuôn mặt phóng to](images/3_mat_phong_to.png)

4. Một đoạn JSON xuất của một người:

   ![JSON export](images/4_json_export.png)

Nguồn ảnh: COCO val2017 / Wikimedia Commons.

## 7. Tự đánh giá

1. Lỗi bạn mắc nhiều nhất hôm nay, và cách bạn sẽ tránh ở dự án thật:
Tự suy đoán ngoài guideline quá nhiều những điểm khuất, không rõ
Chưa có thói quen save thường xuyên, xảy ra hiện tượng mất progress khi máy gặp sự cố.
   ...

2. Một quy tắc bạn đề xuất thêm vào guideline (kèm ảnh ví dụ nếu có):
Phân định rõ hơn khi có một bộ phận bị che khuất hoàn toàn, và bị hình ảnh khác phản chiếu vào khiến việc suy đoán là bất khả thi.
   ...

3. Nhãn của bạn đi vào model ở đâu? Chọn một lỗi bạn đã sửa và nói nó sẽ làm model học sai thế nào (heatmap, trọng số trong loss, hay bước lật ảnh):
Các điểm v > 0 góp phần vào heatmap, cũng như model sẽ học theo các vị trí được đặt, khi v = 0 thì model không học gì ở đó, khi tăng dữ liệu, code lật ngang ảnh và đổi tên `left_*` ↔ `right_*`. Một lỗi đã sửa là vis_flag, khớp thấy được mà để v = 0 sẽ làm trọng số loss khiến model mất một ví dụ.
   ...

## 8. Khó khăn và lỗi kỹ thuật

Chưa có.
...

## Bonus (nếu làm)

### B1 — 3 ảnh người khó thêm

| Ảnh              | Số skeleton | Số người dưới 60 px | Ca khó nhất                                                                                 |
| ---------------- | ----------: | ------------------: | ------------------------------------------------------------------------------------------- |
| 000000104800.jpg |           2 |                   1 | người #2 quay mặt, góc đen kết hợp đồ đen.                                                  |
| 000000161603.jpg |           3 |                   1 | khó cả hình do hình rất mờ và người ở rất xa, mặc đồ khớp màu với khung cảnh khó phân biệt. |
| 000000357549.jpg |           3 |                   0 | người #3 bị che khuất khá nhiều.                                                            |

Kết quả `src/check_submission.py` cho `HoVaTen_bonus_persons.zip`:

```text
- File person: VoDuyThanh_bonus_persons.zip
  Số ảnh: 3 · số skeleton `person`: 8 · mỗi annotation 51 số
  Skeleton theo ảnh: 000000104800=2, 000000161603=3, 000000357549=3
  Cờ v: v=2 61 (45%) · v=1 7 (5%) · v=0 68 (50%)
  num_keypoints trung bình: 8.5
- File face: VoDuyThanh_bonus_faces.zip
  Số ảnh: 5 · số skeleton `face`: 5 · mỗi annotation 39 số
  Skeleton theo ảnh: face_300200=1, face_317330=1, face_45276=1, face_494518=1, face_68290=1
  Cờ v: v=2 48 (74%) · v=1 13 (20%) · v=0 4 (6%)
  num_keypoints trung bình: 12.2
- Ghi chú: 72 điểm v = 0 vẫn mang tọa độ cũ (CVAT 2.x xuất như vậy; chuẩn COCO ghi 0, 0). Không phải lỗi: điểm v = 0 bị bỏ qua khi huấn luyện và khi chấm.
- Số [LỖI]: 0 · số [CẢNH BÁO]: 6
Kết quả: ĐẠT (đọc lại từng cảnh báo ở trên)
```

### B2 — 5 ảnh khuôn mặt đen trắng / hồng ngoại

Ảnh không màu khó hơn ở điểm nào? Kính râm trên ảnh hồng ngoại có còn là `v = 1` không? ảnh không màu sẽ khó hơn ở vùng môi nếu ảnh mặt có râu che khuất phần môi gây khó khăn cho việc gán, và kính râm trên ảnh hồng ngoại sẽ không còn là v = 1 nữa mà sẽ là v = 0.

...

### B3 — Model so với nhãn của tôi (không tính điểm)

- Demo đã dùng:
- Ảnh đã thử:

1. Model có trả điểm cho khớp bị che, hay khớp ngoài ảnh không? Confidence ở các điểm đó thế nào?

   ...

2. Với người quay lưng, model có đổi trái/phải không?

   ...

3. Bộ điểm của model có giống 17 điểm COCO không?

   ...

## 9. Tài liệu tham khảo và công cụ AI đã dùng

Không có
...
