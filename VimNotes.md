Ok, toàn bộ pipeline build .deb đã có sẵn trong `build-deb.sh`. Các bước cụ thể:

## Cách build .deb

### 1. Yêu cầu
- `npm` (Node.js)
- `python3` (cho server phục vụ web local)
- `imagemagick` (lệnh `convert`) để sinh icon các kích thước

### 2. Chạy

```bash
cd /home/anhtuan/Apps/ViNotes

# Build với version mặc định 0.1.0
./build-deb.sh

# Hoặc chỉ định version
./build-deb.sh 1.2.0
```

### 3. Script làm gì

![4712814b-8a6a-450c-b221-6b8d50b81d8a.png](images/4712814b-8a6a-450c-b221-6b8d50b81d8a.png)

| Bước | Mô tả | Output |
|---|---|---|
| `npm run build` | Build web production (Vite) vào `dist/` | `.js`, `.css`, PWA files |
| Dựng cây đóng gói | Tạo cấu trúc thư mục Debian trong `/tmp/vimnotes-deb/vimnotes/` | `usr/share/vimnotes`, `usr/bin`, `DEBIAN`, icons… |
| Copy file | Web app → `usr/share/vimnotes/`, server Python → `server.py` |
| Icon | `convert` PWA icon thành 48/64/128/256/512px + SVG | `/usr/share/icons/hicolor/*/apps/vimnotes.png` |
| Launcher & .desktop | Shell script `vimnotes` + desktop entry | `usr/bin/vimnotes`, `usr/share/applications/vimnotes.desktop` |
| Control & scripts | Metainfo Debian | `DEBIAN/control`, `postinst`, `prerm` |
| Đóng gói | `dpkg-deb --build` | `release/vimnotes_{version}_all.deb` |

### 4. File đầu ra

```
release/vimnotes_0.1.0_all.deb
```

### 5. Cài đặt

```bash
# Bằng apt (đề xuất — tự xử lý dependencies)
sudo apt install ./release/vimnotes_0.1.0_all.deb

# Hoặc dpkg thuần
sudo dpkg -i release/vimnotes_0.1.0_all.deb
# Nếu thiếu dependencies:
sudo apt install -f
```

### 6. Cấu trúc trong .deb

| Đường dẫn | Loại | Chức năng |
|---|---|---|
| `/usr/share/vimnotes/` | thư mục | Web app (index.html, assets…) |
| `/usr/share/vimnotes/server.py` | Python script | HTTP server local: serve static + `/__ai_proxy` (proxy CORS cho AI API) |
| `/usr/bin/vimnotes` | shell script | Launcher: start server (port 8642) → mở trình duyệt (--app của Chrome hoặc Firefox) |
| `/usr/share/applications/vimnotes.desktop` | .desktop | Menu entry (Start Menu, GNOME, KDE…) |
| `/usr/share/icons/hicolor/*/apps/vimnotes.png` | icon | Icon ứng dụng các kích thước |
| `/usr/share/icons/hicolor/scalable/apps/vimnotes.svg` | icon SVG | Icon vector |

### 7. Ghi chú

- **Port**: server chạy ở `http://127.0.0.1:8642`
- **Trình duyệt**: ưu tiên Chrome/Chromium `--app=` mode (cửa sổ viền chỉ có toolbar tối thiểu), fallback Firefox, fallback xdg-open
- **Launcher idempotent**: nếu server đã chạy thì chỉ mở trình duyệt, không start dư
- **prerm**: dọn server Python khi gỡ gói (thủ công, dùng `pkill`)
- **Dependency**: `python3` (bắt buộc), `google-chrome-stable | chromium-browser | chromium | firefox-esr | firefox` (khuyến nghị)
- **AI Proxy**: `POST /__ai_proxy` trên local server — dùng để gọi API AI mà không bị chặn CORS ở phía client