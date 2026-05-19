# FHSS Trade-off Explorer

Bài thực hành Labtainers khảo sát trade-off của kỹ thuật FHSS-MFSK trong giấu tin âm thanh.

---

## Mục tiêu

Sinh viên sẽ:

- Tự tạo nhiều cấu hình FHSS khác nhau
- Quan sát phổ tín hiệu bằng Sonic Visualiser
- So sánh chất lượng giữa các cấu hình
- Phân tích trade-off giữa:
  - BER
  - PSNR
  - Capacity
- Chọn cấu hình phù hợp cho từng kịch bản ứng dụng thực tế

---

## Nội dung chính

Bài lab khảo sát các tham số:

- FHSS hop rate — tốc độ nhảy tần
- MFSK order `m` — số mức tần số
- PSNR — mức độ biến dạng âm thanh
- BER — tỷ lệ lỗi bit
- Capacity — dung lượng nhúng dữ liệu

Đồng thời đánh giá các cấu hình theo:

- Military communication
- VoIP hidden channel
- Radio watermarking

---

## Tải bài lab

```bash
imodule https://github.com/BachTG1505/fhss-tradeoff-explorer/raw/main/fhss-tradeoff-explorer.tar
```

---

## Chạy bài lab

```bash
cd ~/labtainer/trunk/scripts/labtainer-student

labtainer fhss-tradeoff-explorer
```

---

# Các nhiệm vụ

## Task 1 — Baseline Configuration

Tạo cấu hình FHSS cơ sở:

```bash
python3 generate_one.py --hop 1 --m 2
```

---

## Task 2 — Spectrum Observation

Quan sát phổ tín hiệu baseline:

```bash
sonic-visualiser stego_hop1_m2.wav &
```

---

## Task 3 — Fast Hop Configuration

Tạo cấu hình nhảy tần nhanh:

```bash
python3 generate_one.py --hop 5 --m 2
```

---

## Task 4 — Fast Hop Spectrum

Quan sát phổ tín hiệu hop nhanh:

```bash
sonic-visualiser stego_hop5_m2.wav &
```

---

## Task 5 — High-order MFSK

Tạo cấu hình MFSK với `m = 8`:

```bash
python3 generate_one.py --hop 1 --m 8
```

---

## Task 6 — MFSK Spectrum Analysis

Quan sát phổ tín hiệu MFSK:

```bash
sonic-visualiser stego_hop1_m8.wav &
```

---

## Task 7 — Generate Full Trade-off Grid

Sinh toàn bộ grid 9 cấu hình:

```bash
python3 generate_grid.py

python3 build_report.py
```

---

## Task 8 — Interactive Quiz

Khởi chạy quiz:

```bash
python3 quiz_server.py &

firefox report.html &
```

### Đáp án kiểm thử

- Q1 → B
- Q2 → C
- Q3 → C

---

## Task 9 — Final Summary

Tổng kết kết quả:

```bash
python3 summary.py
```

---

# Ý nghĩa bài lab

Bài lab cho thấy:

> Không tồn tại một cấu hình FHSS tối ưu cho mọi trường hợp.

Sinh viên cần lựa chọn tham số dựa trên mục tiêu thực tế:

| Kịch bản | Ưu tiên |
|---|---|
| Military communication | BER thấp |
| VoIP hidden channel | Capacity cao |
| Radio watermark | Cân bằng PSNR / BER / Capacity |

---

# Công cụ sử dụng

- Python 3
- NumPy
- SciPy
- Sonic Visualiser
- Matplotlib

---

# Kiến thức đạt được

- Frequency Hopping Spread Spectrum (FHSS)
- MFSK modulation
- Audio steganography
- Trade-off analysis
- Signal robustness
- Spectrum analysis
- BER vs PSNR optimization

---

# Tác giả

- Họ tên: **Trương Gia Bách**
- Mã sinh viên: **B22DCAT024**
- Lớp: **D22CQAT04-B**
- Học phần: **INT14102 – Kỹ thuật ẩn**
- Giảng viên hướng dẫn: **PGS.TS. Đỗ Xuân Chợ**

