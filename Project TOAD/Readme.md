# 🐸 TOAD Education App

> **TOAD** = Teaching Offline/Online for Areas in Development

An offline-first mobile education platform designed for students in rural areas with limited internet connectivity.

<img width="911" height="915" alt="image" src="https://github.com/user-attachments/assets/f94246bb-234c-4dea-92cf-98ad32f0fd3c" />

---

## 🎯 Problem Statement

Children in rural areas face significant educational challenges:

- **Limited/No Internet** – Expensive data, poor connectivity
- **Lack of Resources** – Few textbooks, no digital devices
- **Low Literacy Rates** – Parents unable to support learning
- **Limited Teacher Access** – Schools understaffed or distant

---

## 💡 Solution

TOAD provides an **offline-first education experience** with 7 core features:

| # | Feature | Description |
|---|---------|-------------|
| 1 | 📊 **Progress Tracking** | Visual dashboard with lessons completed, points, streaks |
| 2 | 🎧 **Audio Learning** | Downloadable audio lessons for low-literacy environments |
| 3 | 🎮 **Game-Based Learning** | Quizzes & mini-games that award points |
| 4 | 👤 **Avatar Customization** | Spend points to unlock outfits & accessories |
| 5 | 💬 **Offline Forum** | Read/write discussions offline; sync when online |
| 6 | 🔍 **Search** | Find lessons, topics, and posts quickly |
| 7 | 📻 **FM/Radio Channel** | Broadcast lessons via radio – zero data required |

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                      📱 Student Device                       │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐      │
│  │  TOAD App   │───▶│Local Storage│◀───│ Sync Engine │      │
│  └─────────────┘    └─────────────┘    └──────┬──────┘      │
└────────────────────────────────────────────────┼────────────┘
                                                 │ When Online
                                                 ▼
┌─────────────────────────────────────────────────────────────┐
│                      ☁️ Cloud Server                         │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐      │
│  │  REST API   │───▶│  Database   │◀───│Sync Service │      │
│  └─────────────┘    └─────────────┘    └─────────────┘      │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                      📻 FM Radio Broadcast                   │
│  ┌─────────────┐    ┌─────────────┐                         │
│  │Radio Station│───▶│Audio Lessons│ ───▶ 🔊 Any Radio Device │
│  └─────────────┘    └─────────────┘                         │
└─────────────────────────────────────────────────────────────┘
```

---

## 👥 Target Users

| User | Need | How TOAD Helps |
|------|------|----------------|
| **Students (6-14)** | Engaging, accessible learning | Gamification, audio, avatars |
| **Teachers** | Track student progress | Dashboard analytics, forums |
| **Volunteers** | Support education | FM broadcasts, offline sharing |
| **Parents** | Monitor learning | Progress reports, badges |

---

## 📂 Project Structure

```
toad-education-app/
├── README.md              # This file
├── docs/
│   ├── REPORT.md          # Full project report
│   └── PRESENTATION.md    # 10-person presentation script
├── assets/
│   ├── toad_storyboard.png
│   └── toad_sketch.png
└── LICENSE
```

---

## 🚀 Roadmap

| Phase | Timeline | Goals |
|-------|----------|-------|
| 1 | Month 1-3 | MVP with 5 core features |
| 2 | Month 4-6 | Add Search & FM Radio |
| 3 | Month 7-9 | Pilot in 3 villages |
| 4 | Month 10-12 | Teacher training & iteration |
| 5 | Year 2 | Scale to 50+ villages |

---

## 🛠️ Tech Stack

- **Frontend**: React Native / Flutter
- **Backend**: Node.js + Express
- **Database**: PostgreSQL + SQLite (local)
- **Storage**: AWS S3 / Firebase
- **Audio**: Lightweight MP3 compression

---

## 📄 Documentation

- [Full Report](docs/REPORT.md)
- [Presentation Script](docs/PRESENTATION.md)

---

## 🤝 Contributing

We welcome contributions! Please read our contributing guidelines before submitting PRs.

---

## 📜 License

MIT License - see [LICENSE](LICENSE) for details.

---

## 📧 Contact

- **Project**: TOAD Education
- **Email**: <toad.education@example.com>
- **Website**: <www.toad-app.org>

---

> *"Bringing education to every child, everywhere – online or offline."* 🐸
