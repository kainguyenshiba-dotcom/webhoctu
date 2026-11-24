# Wordwell — IELTS Vocabulary

Website học từ vựng tiếng Anh theo chủ đề, nội dung mẫu lấy từ PDF IELTS Writing & Speaking bạn gửi. Ứng dụng dùng Vite + React; tài khoản và dữ liệu tiến độ lưu bằng Supabase Auth và Postgres. Nếu chưa kết nối Supabase, tiến độ vẫn được lưu cục bộ trong trình duyệt để dùng thử.

## Chạy trên máy

1. Cài Node.js bản LTS nếu máy chưa có.
2. Mở terminal tại thư mục website và chạy `npm install`.
3. Chạy `npm run dev`, rồi mở địa chỉ Vite hiện trong terminal.

## Bật đăng nhập và đồng bộ tiến độ

1. Tạo project tại [supabase.com](https://supabase.com/) và mở **SQL Editor**.
2. Dán rồi chạy nội dung file `supabase/schema.sql`. Bảng lưu dữ liệu có chính sách RLS để mỗi tài khoản chỉ đọc/ghi tiến độ của chính mình.
3. Trong **Project Settings → API**, sao chép Project URL và public anon/publishable key. Không đưa `service_role` key vào website.
4. Tạo file `.env.local` ở thư mục gốc, theo mẫu:

   ```env
   VITE_SUPABASE_URL=https://your-project.supabase.co
   VITE_SUPABASE_ANON_KEY=your-public-anon-key
   ```

5. Khởi động lại `npm run dev`, chọn **Đăng nhập → Đăng ký** để tạo tài khoản. Tiến độ sẽ đồng bộ vào Supabase sau khi đăng nhập.

## Deploy lên Vercel

1. Đưa thư mục này lên GitHub rồi vào [vercel.com](https://vercel.com/) → **Add New → Project** và import repository.
2. Vercel tự nhận cấu hình Vite. Build command: `npm run build`; output directory: `dist`.
3. Trong **Project → Settings → Environment Variables**, thêm `VITE_SUPABASE_URL` và `VITE_SUPABASE_ANON_KEY` giống `.env.local`.
4. Deploy hoặc redeploy sau khi thêm biến môi trường.
5. Trong Supabase **Authentication → URL Configuration**, đặt Site URL là domain Vercel, ví dụ `https://ten-du-an.vercel.app`. Thêm domain đó vào Redirect URLs nếu cần.

Mật khẩu và dữ liệu cá nhân không được lưu trong localStorage. Chế độ chưa đăng nhập chỉ lưu tiến độ học trên trình duyệt hiện tại. Khi tạo tài khoản, website đọc/ghi tiến độ tài khoản vào Supabase.

## Trải nghiệm học

- 7 bộ từ mẫu, gồm Education, Technology & AI, Environment, Health & lifestyle, Work & careers, Money & consumption, Travel & tourism.
- Mỗi thẻ có nghĩa tiếng Việt, phiên âm IPA và ví dụ; nút loa dùng giọng đọc tiếng Anh của trình duyệt.
- Matching và multiple choice lấy từ đến hạn để ôn. Trả lời đúng đưa từ vào lịch ôn cách quãng; trả lời sai sẽ giữ từ đến hạn hôm nay.
- Học từ mới bị chặn nếu còn từ cũ đến hạn. Dashboard hiển thị số từ đã học, từ cần ôn, chuỗi ngày học và heatmap theo năm.
