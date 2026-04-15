# CSC4005 – Lab 1 Report Template

## 1. Mục tiêu
Huấn luyện mô hình MLP để phân loại 6 loại lỗi bề mặt thép từ bộ dữ liệu NEU. Tìm hiểu ảnh hưởng của Optimizer và Regularization (Dropout) đến hiệu suất mô hình.

## 2. Cấu hình thí nghiệm
Tham số	Run 1 (Baseline)	Run 2 (SGD)	Run 3 (Dropout)
Optimizer	AdamW	SGD	AdamW
Learning Rate	0.001	0.01	0.001
Dropout	0	0	0.3
Epochs	20	20	20.

## 3. Kết quả

Link W&B: https://wandb.ai/datn89367-i-h-c-i-nam/csc4005-lab1-neu-mlp?nw=nwuserdatn89367

Cấu hình (Run Name)	Optimizer	Learning Rate	Dropout	Best Val Acc	Test Acc (Final)
debug_run (Baseline)	AdamW	0.001	0.0	0.4593	0.4556
sgd_run	SGD	0.01	0.0	0.4333	0.4259
dropout_run	AdamW	0.001	0.3	0.4593	0.4556

![Learning Curves](outputs/figures/learning_curves.png)

## 4. Phân tích
- Cấu hình nào tốt nhất?
    Cấu hình AdamW (Run 1 & 3) tốt nhất vì đạt độ chính xác cao nhất (45.56%) và quá trình huấn luyện diễn ra ổn định.
- Dấu hiệu overfitting / underfitting là gì?
    Mô hình đang bị Underfitting vì độ chính xác trên cả tập Train và Validation đều thấp (~45%). Đường Loss của Train và Validation vẫn đi sát nhau, chưa có sự phân kỳ, chứng tỏ mô hình chưa đủ phức tạp để học hết đặc trưng của dữ liệu hoặc cần chạy nhiều Epoch hơn.
- AdamW và SGD khác nhau ra sao trong thí nghiệm của bạn?
    AdamW hội tụ mượt mà và ổn định hơn. SGD dao động rất mạnh (biểu đồ hình răng cưa) và đạt kết quả thấp hơn một chút trong thí nghiệm này.

## 5. Kết luận

## 5. Kết luận
Dựa trên kết quả thực nghiệm từ 3 cấu hình, em chọn cấu hình **Run 1 (Baseline - AdamW)** là cấu hình tốt nhất cho bài toán này với các lý do sau:

1. **Hiệu năng và độ ổn định:** AdamW cho kết quả Test Accuracy cao nhất (45.56%). So với SGD, AdamW giúp mô hình hội tụ mượt mà hơn, đường Loss không bị dao động cực đoan, giúp việc kiểm soát quá trình huấn luyện dễ dàng hơn.
2. **Khả năng tổng quát hóa:** Việc thêm Dropout 0.3 ở Run 3 chưa mang lại cải thiện rõ rệt, chứng tỏ với kiến trúc MLP đơn giản hiện tại, mô hình chưa đủ phức tạp để bị overfitting. Do đó, cấu hình baseline vẫn là lựa chọn tối ưu về mặt chi phí tính toán.


