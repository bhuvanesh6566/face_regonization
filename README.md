# Face Attendance System

A complete face recognition-based attendance system with a modern web interface. Register users with their photos, then mark attendance using face recognition.

## 🚀 Quick Start

### Prerequisites

- **Python 3.8+** installed
- **MySQL** installed and running
- **Webcam** (for marking attendance)

### Step 1: Install Dependencies

```bash
cd face_attendance_backend
pip install -r requirements.txt
```

**Note:** Installing `face-recognition` and `dlib` may take a few minutes. On Windows, you might need Visual C++ Build Tools.

### Step 2: Setup Database

1. **Update MySQL password** in `face_attendance_backend/setup_database.py`:
   ```python
   DB_PASS = "your_mysql_password"  # Change this
   ```

2. **Create the database**:
   ```bash
   cd face_attendance_backend
   python setup_database.py
   ```

3. **Update config.py** with the same MySQL credentials:
   ```python
   SQLALCHEMY_DATABASE_URI = 'mysql+pymysql://root:your_password@localhost/face_attendance'
   ```

4. **Verify configuration**:
   ```bash
   python check_config.py
   ```

### Step 3: Start Backend

**Option A - Double-click (Windows):**
- Double-click `face_attendance_backend/run_backend.bat`

**Option B - Command line:**
```bash
cd face_attendance_backend
python app.py
```

You should see:
```
✓ Database tables created/verified successfully
 * Running on http://127.0.0.1:5000
```

**Keep this terminal open!**

### Step 4: Open Frontend

**Option A - Direct file:**
- Open `frontend/index.html` in your browser (Chrome/Edge recommended)

**Option B - Local server (recommended):**
```bash
cd frontend
python -m http.server 8080
```
Then open: **http://localhost:8080**

---

## 📁 Project Structure

```
face recognization/
├── face_attendance_backend/     # Flask API backend
│   ├── app.py                   # Main Flask application
│   ├── models.py                # Database models (User, Attendance)
│   ├── utils.py                 # Face recognition utilities
│   ├── config.py                # Database configuration
│   ├── setup_database.py        # Database setup script
│   ├── check_config.py          # Configuration checker
│   ├── run_backend.bat          # Windows startup script
│   └── requirements.txt          # Python dependencies
│
└── frontend/                    # Web UI
    ├── index.html               # Main HTML page
    ├── css/
    │   └── styles.css           # Styling
    ├── js/
    │   └── app.js               # Frontend logic
    └── README.md                # Frontend instructions
```

---

## 🎯 Features

### 1. **Register Users**
- Enter name and email
- Upload a clear face photo (one face per image)
- Face encoding is stored in the database

### 2. **Mark Attendance**
- Use webcam to capture your face
- Or upload an image file
- System recognizes registered users automatically
- Prevents duplicate attendance for the same day

### 3. **View Logs**
- See all attendance records
- Shows user name and timestamp
- Sorted by most recent first

---

## 🔧 API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/` | GET | Health check |
| `/health` | GET | Detailed health status |
| `/register` | POST | Register new user (name, email, image) |
| `/mark_attendance` | POST | Mark attendance (image) |
| `/logs` | GET | Get attendance logs |
| `/users` | GET | Get list of registered users |

---

## 🐛 Troubleshooting

### Backend won't start

**Error: "ModuleNotFoundError"**
```bash
pip install -r requirements.txt
```

**Error: "Can't connect to MySQL"**
- Make sure MySQL is running
- Check `config.py` has correct credentials
- Run `python check_config.py` to verify

**Error: "Database doesn't exist"**
```bash
python setup_database.py
```

### Frontend shows "Cannot reach server"

- Make sure backend is running (check terminal)
- Backend should be on `http://localhost:5000`
- Check browser console for errors
- Try opening backend URL directly: `http://localhost:5000/health`

### Face recognition not working

- Make sure photo has **one clear face**
- Good lighting helps
- Try different angles/expressions
- Check backend terminal for error messages

### "User not recognized"

- User must be registered first
- Use a clear, front-facing photo
- Ensure good lighting when marking attendance
- Try registering with multiple photos if needed

---

## 📝 Configuration

### Database Settings

Edit `face_attendance_backend/config.py`:
```python
SQLALCHEMY_DATABASE_URI = 'mysql+pymysql://username:password@host/database'
```

### Change Backend Port

Edit `face_attendance_backend/app.py` (last line):
```python
app.run(debug=True, port=5000)  # Change 5000 to your port
```

Then update `frontend/js/app.js`:
```javascript
const API_BASE = 'http://localhost:YOUR_PORT';
```

---

## 🛠️ Development

### Database Management

Use `manage_db.py` to view/manage users:
```bash
python manage_db.py
```

### Testing Backend

Test endpoints with curl or Postman:
```bash
# Health check
curl http://localhost:5000/health

# Get logs
curl http://localhost:5000/logs
```

---

## 📄 License

This project is open source and available for educational purposes.

---

## 💡 Tips

- **Registration:** Use high-quality photos with good lighting
- **Attendance:** Face the camera directly for best results
- **Database:** Backup your MySQL database regularly
- **Performance:** System works best with < 100 registered users

---

## 🆘 Need Help?

1. Check the **Troubleshooting** section above
2. Verify backend is running: `http://localhost:5000/health`
3. Check browser console (F12) for frontend errors
4. Check backend terminal for server errors

---

**Made with ❤️ for automated attendance tracking**
