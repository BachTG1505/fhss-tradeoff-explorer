cat > README.md << 'EOF'
# FHSS Trade-off Explorer

Bài thực hành Labtainers khảo sát sự thay đổi của các chỉ số PSNR, BER và Capacity theo Hop Rate và MFSK Order trong giấu tin âm thanh FHSS-MFSK.

---

## Mục tiêu

Sinh viên sẽ:

- Tự tạo các cấu hình FHSS-MFSK khác nhau
- Quan sát phổ tín hiệu qua ảnh spectrogram trong báo cáo HTML
- Có thể mở Sonic Visualiser để quan sát trực tiếp nếu môi trường X11 hỗ trợ
- So sánh chất lượng giữa các cấu hình
- Phân tích trade-off giữa:
  - PSNR
  - BER
  - Capacity
- Chọn cấu hình phù hợp cho từng kịch bản ứng dụng thực tế

---

## Nội dung chính

Bài lab khảo sát các tham số:

- Hop Rate: tốc độ nhảy tần của chuỗi FHSS
- MFSK Order `m`: số mức tần số dùng để biểu diễn dữ liệu
- PSNR: mức độ biến dạng âm thanh sau khi nhúng tin
- BER: tỷ lệ lỗi bit sau khi trích xuất
- Capacity: dung lượng nhúng dữ liệu

Bài lab đánh giá các cấu hình theo 3 kịch bản:

- Military communication: ưu tiên BER thấp
- VoIP hidden channel: ưu tiên Capacity cao
- Radio watermarking: cân bằng PSNR, BER và Capacity

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

## Task 1 - Tạo cấu hình baseline

```bash
python3 generate_one.py --hop 1 --m 2
```

Cấu hình này dùng Hop Rate thấp và MFSK bậc 2 để làm mốc so sánh.

---

## Task 2 - Quan sát phổ baseline

Nếu Sonic Visualiser mở được:

```bash
sonic-visualiser stego_hop1_m2.wav &
```

Nếu môi trường X11 không hỗ trợ Sonic, sinh viên quan sát phổ trong `report.html` sau Task 7.

---

## Task 3 - Tạo cấu hình hop nhanh

```bash
python3 generate_one.py --hop 5 --m 2
```

Cấu hình này giữ `m = 2` nhưng tăng Hop Rate để quan sát ảnh hưởng của tốc độ nhảy tần.

---

## Task 4 - Quan sát phổ hop nhanh

```bash
sonic-visualiser stego_hop5_m2.wav &
```

Nếu Sonic lỗi do X11, quan sát ảnh `spec_hop5_m2.png` trong `report.html`.

---

## Task 5 - Tạo cấu hình MFSK bậc cao

```bash
python3 generate_one.py --hop 1 --m 8
```

Cấu hình này giữ Hop Rate thấp nhưng tăng `m = 8` để khảo sát ảnh hưởng của MFSK Order tới Capacity.

---

## Task 6 - Quan sát phổ MFSK

```bash
sonic-visualiser stego_hop1_m8.wav &
```

Nếu Sonic lỗi do X11, quan sát ảnh `spec_hop1_m8.png` trong `report.html`.

---

## Task 7 - Sinh grid 9 cấu hình và báo cáo HTML

```bash
python3 generate_grid.py

python3 build_report.py
```

Lệnh này sinh:

- 9 file audio stego
- 9 ảnh spectrogram
- `data.json`
- `report.html`

---

## Task 8 - Trả lời quiz tương tác

```bash
python3 quiz_server.py &

firefox report.html &
```

### Đáp án kiểm thử

- Q1: B
- Q2: C
- Q3: C

---

## Task 9 - Tổng kết

```bash
python3 summary.py
```

---

# Ghi chú về Sonic Visualiser

Sonic Visualiser là công cụ GUI nên phụ thuộc cấu hình X11 của Labtainer/VM.

Nếu gặp lỗi:

```text
qt.qpa.xcb: could not connect to display :0
```

có thể xử lý trên host bằng:

```bash
cd ~/labtainer/trunk/scripts/labtainer-student

stoplab

xhost +local:

labtainer fhss-tradeoff-explorer
```

Nếu vẫn lỗi, sinh viên có thể dùng `report.html` để quan sát spectrogram thay thế.

---

# Ý nghĩa bài lab

Bài lab cho thấy:

> Không tồn tại một cấu hình FHSS-MFSK tối ưu cho mọi trường hợp.

Sinh viên cần lựa chọn tham số theo mục tiêu thực tế:

| Kịch bản | Ưu tiên |
|---|---|
| Military communication | BER thấp |
| VoIP hidden channel | Capacity cao |
| Radio watermarking | Cân bằng PSNR / BER / Capacity |

---

# Công cụ sử dụng

- Python 3
- NumPy
- Sonic Visualiser
- Firefox
- Labtainers

---

# Kiến thức đạt được

- Frequency Hopping Spread Spectrum
- MFSK modulation
- Audio steganography
- Spectrum analysis
- Trade-off giữa PSNR, BER và Capacity
- Lựa chọn cấu hình theo kịch bản ứng dụng

---

# Tác giả

- Họ tên: **Trương Gia Bách**
- Mã sinh viên: **B22DCAT024**
- Lớp: **D22CQAT04-B**
- Học phần: **INT14102 - Kỹ thuật ẩn**
- Giảng viên hướng dẫn: **PGS.TS. Đỗ Xuân Chợ**

EOF
