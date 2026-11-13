# Báo cáo cá nhân — TranThoLam-2A202603025

Dữ liệu: 12 ảnh người COCO val2017 (Lin et al., 2014) và 8 ảnh chân dung Wikimedia Commons, chỉ dùng trong lớp.

## 0. Thông tin học viên

- Họ tên: Trần Thọ Lâm
- MSSV: 2A202603025
- Email: trantholam29@gmail.com
- Link repository: https://github.com/trantholam2k4/K5-L2-DAY04-TranThoLam-2A202603025-KeypointPose
- Phiên bản CVAT (Help → About): v2.74.1
- Máy: hệ điều hành Windows (WSL2) · RAM 16 GB · chạy CVAT chế độ đầy đủ 
- Bộ ảnh (`src/exports/assignment.json` do `lab.py setup` tạo): có
- Giờ bắt đầu: 17:00 12/11/2026
- Giờ kết thúc: 12:00 13/11/2026

## 1. Kiểm tra label (CP0)

| Label | Kiểu | Số điểm | Tên điểm đúng bảng của lab? | Đúng thứ tự? | Số cạnh |
|---|---|---:|---|---|---:|
| `person` | `skeleton` | 17 | Có (`nose` → `right_ankle`) | Có (1 → 17) | 19 |
| `face` | `skeleton` | 13 | Có (`left_eye_outer` → `lip_lower`) | Có (1 → 13) | 13 |

Mẫu `person` dựng theo người quay mặt về camera (các điểm `left_*` nằm bên phải khung mẫu)? **Có**

Cách đổi cờ `occluded` / `outside` cho **một điểm** trên phiên bản CVAT này (một câu):

Nhấp chọn điểm khớp cần chỉnh (hoặc trỏ chuột vào điểm đó), sau đó bấm biểu tượng hình con mắt gạch chéo (**Switch occluded property**, phím tắt `Q`) trên thanh thuộc tính/menu ngữ cảnh của điểm để bật `occluded` (`v = 1`), hoặc bấm biểu tượng hình chữ nhật mũi tên ra ngoài (**Switch outside property**, phím tắt `O`) để bật `outside` (`v = 0`).

## 2. Số lượng đã gán và thời gian (CP1, CP2)

| Nhóm ảnh | Số ảnh | Số skeleton đã gán | Số người dưới 60 px (không gán) | Số poster / gương / màn hình bỏ qua | Thời gian (phút) |
|---|---:|---:|---:|---:|---:|
| `easy` | 5 | 5 | 0 | 0 | 115 |
| `occluded` | 3 | 6 | 0 | 0 | 45 |
| `back` | 2 | 4 | 0 | 0 | 30 |
| `small` | 1 | 3 | 4 | 0 | 20 |
| `crowd` | 1 | 3 | 0 | 0 | 20 |
| `faces` | 8 | 8 | — | 0 | 45 |

- Số ảnh người đã xong ở mốc phút 105: 4 / 12
- Thời gian thực tế (phút): CP1 230 · CP2 45 · CP3 25
- Ảnh tốn thời gian nhất là ảnh nào, vì sao?

Ảnh tốn thời gian nhất là `000000269462.jpg` (nhóm `small`, 3 skeleton cảnh sát cưỡi ngựa và bỏ qua 4 người đi bộ `< 60 px` ở vỉa hè bên trái) và `000000381889.jpg` (nhóm `crowd`, 3 skeleton quanh bàn tiệc) vì có nhiều nhân vật đan xen, các khớp chân bị che khuất bởi bàn bánh cưới hoặc cắt ngang mép dưới ảnh (`y = 640.0`) cần phóng to kiểm tra từng điểm và gắn cờ visibility.

## 3. Bảng ca khó (CP1, CP2)

Mỗi điểm bạn phân vân một dòng, nhất là phân vân giữa `v = 1` và `v = 0`, hoặc không chắc hướng người.

| Ảnh | Người / mặt | Điểm | Cờ đã chọn | Phân vân giữa | Lý do chọn |
|---|---|---|---:|---|---|
| `000000381889.jpg` | Người #1 (`id: 13`) | `left_ankle`, `right_ankle` | `outside` (`v = 0`) | `v = 1` và `v = 0` | <Điền lý do thực tế của bạn> |
| `000000381889.jpg` | Người #3 (`id: 15`) | `left_knee`, `right_knee`, `left_ankle` | `outside` (`v = 0`) | `v = 1` và `v = 0` | <Điền lý do thực tế của bạn> |
| `000000189365.jpg` | Người #2 (`id: 8`) | `left_eye`, `right_eye` | `outside` (`v = 0`) | `v = 1` và `v = 0` | <Điền lý do thực tế của bạn> |
| `000000558066.jpg` | Người #1 (`id: 21`) | `left_ankle`, `right_ankle` | `outside` (`v = 0`) | `v = 1` và `v = 0` | <Điền lý do thực tế của bạn> |

## 4. Bảng tự review (CP3)

Đi từ ảnh cuối về ảnh đầu. 5 ảnh người (ít nhất 2 ảnh `back` hoặc `crowd`) và 3 ảnh mặt. Ít nhất 8 dòng, kể cả dòng `ok`. Ghi lỗi trước, sửa sau.

Mã lỗi dùng đúng một trong: `lr_swap`, `vis_flag`, `position`, `missing`, `extra`, `ok`.

| Ảnh | Người / mặt | Điểm | Mã lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|---|
| `000000558066.jpg` | Người #1 (`id: 21`) | `left_ankle`, `right_ankle` | `ok` | Đã kiểm tra 17 điểm, hai cổ chân ngoài khung gắn `outside` (`v = 0`). | <Rồi / Không cần sửa> |
| `000000469061.jpg` | Người #2 (`id: 19`) | `left_knee`, `right_knee` | `lr_swap` | `check_submission.py` cảnh báo trái/phải giữa cặp vai và gối chưa nhất quán. | <Rồi / Chưa> |
| `000000461002.jpg` | Người #1, #2 (`id: 16, 17`) | Toàn bộ `left_*`/`right_*` | `lr_swap` | `check_submission.py` cảnh báo ngược trái/phải ở nhân vật #2 và cặp gối/cổ chân #1. | <Rồi / Chưa> |
| `000000381889.jpg` | Người #3 (`id: 15`) | `right_ankle` | `vis_flag` | Điểm `right_ankle` tại `(114.9, 639.1)` sát mép dưới ảnh đang để `v = 2` thay vì `outside`. | <Rồi / Chưa> |
| `000000269462.jpg` | Người #1, #2, #3 (`id: 10–12`) | Toàn bộ `left_*`/`right_*` | `lr_swap` | `check_submission.py` cảnh báo 3 người quay mặt về camera nhưng điểm `left` nằm bên trái ảnh. | <Rồi / Chưa> |
| `face_79591.jpg` | Mặt #1 (`id: 8`) | `left_eye_*`, `right_eye_*` | `lr_swap` | `check_submission.py` cảnh báo cụm `left_eye_*` nằm bên trái ảnh (`x = 124.0`). | <Rồi / Chưa> |
| `face_362568.jpg` | Mặt #1 (`id: 3`) | 13 điểm khuôn mặt | `ok` | Không có cảnh báo, cụm `left_eye_*` nằm đúng bên phải ảnh (`x = 342.16`). | <Rồi / Không cần sửa> |
| `face_196742.jpg` | Mặt #1 (`id: 1`) | `left_eye_*`, `mouth_left` | `lr_swap` | `check_submission.py` cảnh báo cụm `left_eye_*` nằm bên trái ảnh (`x = 180.2`). | <Rồi / Chưa> |

Tổng hợp số lỗi theo mã:

| `lr_swap` | `vis_flag` | `position` | `missing` | `extra` | `ok` |
|---:|---:|---:|---:|---:|---:|
| 5 | 1 | 0 | 0 | 0 | 2 |

Điểm còn phân vân giữa `v = 1` và `v = 0` (ghi cả hai lựa chọn và lý do chọn):

<Điền điểm cụ thể bạn còn phân vân giữa v = 1 và v = 0 và lý do chọn của bạn>

## 5. Kiểm file xuất và kết quả tự kiểm (CP4)

Tự kiểm tay trong file JSON:

| File | Người / mặt kiểm (ảnh, thứ tự) | Số phần tử `keypoints` | Điểm `outside` ra `v = 0`, `occluded` ra `v = 1`? | `num_keypoints` khớp? |
|---|---|---:|---|---|
| `TranThoLam_persons.zip` | `000000043500.jpg` (`id: 1`, người #1) | 51 (17 × 3) | Có (toàn bộ 17 điểm đều `v = 2`) | Có (`num_keypoints: 17`) |
| `TranThoLam_persons.zip` | `000000381889.jpg` (`id: 13`, người #1) | 51 (17 × 3) | Có (2 điểm `left_ankle`, `right_ankle` ra `v = 0`) | Có (`num_keypoints: 15`) |
| `TranThoLam_faces.zip` | `face_196742.jpg` (`id: 1`, mặt #1) | 39 (13 × 3) | Có (toàn bộ 13 điểm đều `v = 2`) | Có (`num_keypoints: 13`) |

Sau khi xuất, CVAT ghi `occluded` thành `v = 1` và `outside` thành `v = 0`. Tọa độ của điểm `outside` trong file là `0, 0` hay tọa độ cũ? **Tọa độ cũ** (ví dụ `[264.7, 640.0, 0]` ở `id: 13` ảnh `000000381889.jpg`, riêng trường hợp tọa độ gốc tại gốc ảnh thì ghi `0.0, 635.7, 0`).

Hai job đã chuyển sang completed trên CVAT? <Có / Không — nhớ chuyển sang completed trên CVAT trước khi điền Có>

Dán phần **TÓM TẮT** in ra từ `src/check_submission.py`:

```text
----- TÓM TẮT (dán vào báo cáo mục 5) -----
- File person: TranThoLam_persons.zip

  Số ảnh: 12 · số skeleton `person`: 21 · mỗi annotation 51 số
  Skeleton theo ảnh: 000000043500=2, 000000156986=2, 000000177889=1, 000000184224=1, 000000189365=2, 000000213933=1, 000000269462=3, 000000381889=3, 000000461002=2, 000000469061=2, 000000525227=1, 000000558066=1
  Cờ v: v=2 347 (97%) · v=1 0 (0%) · v=0 10 (3%)
  num_keypoints trung bình: 16.5
- File face: TranThoLam_faces.zip

  Số ảnh: 8 · số skeleton `face`: 8 · mỗi annotation 39 số
  Skeleton theo ảnh: face_196742=1, face_296767=1, face_362568=1, face_416730=1, face_425647=1, face_496353=1, face_79367=1, face_79591=1
  Cờ v: v=2 104 (100%) · v=1 0 (0%) · v=0 0 (0%)
  num_keypoints trung bình: 13.0
- Ghi chú: 10 điểm v = 0 vẫn mang tọa độ cũ (CVAT 2.x xuất như vậy; chuẩn COCO ghi 0, 0). Không phải lỗi: điểm v = 0 bị bỏ qua khi huấn luyện và khi chấm.

- Số [LỖI]: 0 · số [CẢNH BÁO]: 15

Kết quả: ĐẠT (đọc lại từng cảnh báo ở trên)