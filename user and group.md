# 🧑‍💻 Quản lý User và Group trong Linux (Ubuntu)

## 📌 1. Tổng quan
- **User**: là tài khoản dùng để đăng nhập vào hệ thống.
- **Group**: là tập hợp các user dùng chung quyền truy cập đến tài nguyên hệ thống.

---

## 🧑‍💻 2. Quản lý User

### ➕ Tạo user mới
```bash
sudo useradd <username>
```

### ➕ Tạo user kèm thư mục home:
```bash
sudo useradd -m <username>
```

### ➕ Tạo user có group chính, group phụ, shell, mô tả:
```bash
sudo useradd -m -g <group> -G <group1,group2> -s /bin/bash -c "Mô tả" <username>
```

---

### 🔐 Đặt mật khẩu cho user:
```bash
sudo passwd <username>
```

---

### ✏️ Thay đổi thông tin user:
```bash
sudo usermod [tùy_chọn] <username>
```

Ví dụ: thay đổi thư mục home:
```bash
sudo usermod -d /home/newhome -m <username>
```

---

### ❌ Xóa user:
```bash
sudo userdel <username>
```

Xóa cả thư mục home:
```bash
sudo userdel -r <username>
```

---

## 📚 Tùy chọn đầy đủ cho `useradd`

| Option               | Mô tả |
|----------------------|------|
| `-m`                 | Tạo thư mục home |
| `-M`                 | Không tạo thư mục home |
| `-d <dir>`           | Chỉ định thư mục home |
| `-s <shell>`         | Chỉ định shell mặc định |
| `-g <group>`         | Nhóm chính |
| `-G <group1,...>`    | Các nhóm phụ |
| `-u <UID>`           | Chỉ định UID |
| `-r`                 | Tạo system user |
| `-c "<comment>"`     | Thêm mô tả |
| `-e <YYYY-MM-DD>`    | Ngày hết hạn tài khoản |
| `-f <days>`          | Số ngày sau hết hạn sẽ bị khóa |
| `-k`                 | Copy từ `/etc/skel` vào home |
| `-N`                 | Không tạo group cùng tên với user |

---

## 📚 Tùy chọn đầy đủ cho `usermod`

| Option               | Mô tả |
|----------------------|------|
| `-c "<comment>"`     | Sửa mô tả |
| `-d <dir>`           | Đổi thư mục home |
| `-m`                 | Di chuyển nội dung thư mục home |
| `-g <group>`         | Đặt lại group chính |
| `-G <group1,...>`    | Gán các group phụ (ghi đè) |
| `-aG <group>`        | Thêm vào group phụ (nên dùng) |
| `-s <shell>`         | Đổi shell |
| `-u <UID>`           | Đổi UID |
| `-l <newname>`       | Đổi tên user |
| `-L`                 | Khóa tài khoản |
| `-U`                 | Mở khóa tài khoản |
| `-e <YYYY-MM-DD>`    | Đặt ngày hết hạn |

---

## 📚 Tùy chọn đầy đủ cho `userdel`

| Option    | Mô tả |
|-----------|------|
| `-r`      | Xóa cả thư mục home |
| `--force` | Bắt buộc xóa (nguy hiểm) |

---

## 👥 3. Quản lý Group

### ➕ Tạo group:
```bash
sudo groupadd <groupname>
```

### ❌ Xóa group:
```bash
sudo groupdel <groupname>
```

### 🔄 Đổi tên group:
```bash
sudo groupmod -n <newname> <oldname>
```

### 🔄 Đổi GID:
```bash
sudo groupmod -g <GID> <groupname>
```

---

## 📚 Tùy chọn đầy đủ cho `groupadd`

| Option     | Mô tả |
|------------|------|
| `-g <GID>` | Chỉ định GID |
| `-f`       | Không báo lỗi nếu group đã tồn tại |
| `-K`       | Ghi đè cấu hình mặc định |

---

## 📚 Tùy chọn đầy đủ cho `groupmod`

| Option        | Mô tả |
|---------------|------|
| `-g <GID>`    | Đổi GID |
| `-n <name>`   | Đổi tên group |

---

## 📋 4. Kiểm tra thông tin

### Kiểm tra thông tin user:
```bash
id <username>
```

### Kiểm tra group của user:
```bash
groups <username>
```

### Xem danh sách user:
```bash
cat /etc/passwd
```

### Xem danh sách group:
```bash
cat /etc/group
```

---

## 📁 5. File hệ thống liên quan

| File              | Vai trò |
|-------------------|--------|
| `/etc/passwd`     | Danh sách user |
| `/etc/shadow`     | Mật khẩu mã hóa |
| `/etc/group`      | Danh sách group |
| `/etc/gshadow`    | Bảo mật group |

---

## 🛠️ 6. Một số ví dụ thực tế

### Tạo user `an` có thư mục home và group chính là `dev`:
```bash
sudo groupadd dev
sudo useradd -m -d /home/an -g dev an
sudo passwd an
```

### Thêm `an` vào group phụ `docker`, `sudo`:
```bash
sudo usermod -aG docker,sudo an
```

### Đổi tên user từ `an` thành `anh`:
```bash
sudo usermod -l anh an
sudo usermod -d /home/anh -m anh
```

---

## ✅ Lưu ý

- Luôn dùng `-m` khi đổi home để giữ dữ liệu.
- Dùng `-aG` thay vì `-G` để tránh mất group phụ.
- Không xóa group đang được làm group chính cho user.
- Dùng `man <lệnh>` để xem thêm hướng dẫn chi tiết.

---

📌 Tài liệu áp dụng cho Ubuntu và hầu hết các bản phân phối Linux khác.
