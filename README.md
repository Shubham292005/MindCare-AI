# 🧠 MindCare-AI - Mental Health & Wellness Platform

**Language:** English | [Hindi](#हिंदी) | [Marathi](#मराठी) | [Tamil](#தமிழ்) | [Telugu](#తెలుగు) | [Kannada](#ಕನ್ನಡ) | [Bengali](#বাংলা) | [Punjabi](#ਪੰਜਾਬੀ)

![MindCare-AI](https://img.shields.io/badge/MindCare-AI-blue?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)
![Status](https://img.shields.io/badge/Status-Active%20Development-orange?style=flat-square)

## 🎯 Mission

To provide accessible, anonymous, AI-powered mental health support in Indian regional languages for students, working professionals, and seniors - with features like mood tracking, crisis intervention, breathing exercises, and 24/7 chatbot support.

---

## ✨ Key Features

### 🤖 **AI Chatbot**
- Available in 10+ Indian languages (Hindi, Marathi, Tamil, Telugu, Kannada, Bengali, Punjabi, English, Gujarati, Urdu)
- Therapy-informed conversations (CBT, mindfulness techniques)
- Anonymous & encrypted chats
- Mood-aware responses
- No fake diagnosis - supportive only
- Offline mode for low-data users

### 📊 **Mood Tracking & Analytics**
- Daily mood logging with emotions
- 7-day, 30-day mood trends
- Mood prediction (AI-powered forecasting)
- Visual mood graphs
- Trigger identification
- Streak tracking for consistency

### 🌬️ **Wellness Tools**
- **Breathing Exercises**: Box breathing, 4-7-8 technique, guided meditation
- **Daily Motivation**: Personalized quotes based on mood
- **Stress Assessments**: Quick stress level check-in
- **Sleep Tips**: Science-backed sleep hygiene advice

### 🚨 **Crisis Management**
- Crisis indicator detection in real-time
- Emergency helpline numbers with auto-dial
- Parent/Guardian notification system
- Safety resources & emergency contacts
- De-escalation techniques
- Anonymous reporting

### 👨‍👩‍👧‍👦 **Family Integration**
- Parent dashboard (for student accounts)
- Alert system for concerning messages
- Customizable notification thresholds
- Non-intrusive monitoring
- Family tips for supporting loved ones

### 🔐 **Privacy & Security**
- End-to-end encrypted chats
- Anonymous mode (no personal data)
- GDPR & India's data protection compliant
- Session timeouts for public devices
- No data sharing with third parties
- Incognito mode support

### 📱 **Multi-Device Support**
- Mobile-first responsive design
- Works on 2G/3G networks
- Offline functionality
- App (iOS/Android)
- Web platform
- Low-bandwidth mode (minimal graphics)

### 🎙️ **Voice Features**
- Alexa-style voice chatbot
- Text-to-speech in regional languages
- Speech-to-text input
- Voice mood logging
- Audio meditation guides

### 👥 **User Types**
1. **Students** (13-18): School stress, exams, peer pressure
2. **Young Adults** (19-30): Career stress, relationships
3. **Professionals** (31-60): Work pressure, burnout, life balance
4. **Seniors** (60+): Retirement adjustment, loneliness, health anxiety
5. **Parents**: Tips for supporting children's mental health

### 📈 **Admin Dashboard**
- User analytics
- Crisis alert monitoring
- Content management
- Feedback reviews
- System health monitoring
- Reports generation

---

## 🛠️ Tech Stack

### **Frontend**
```
React.js (TypeScript)
Tailwind CSS
Redux (State Management)
React Query (Data Fetching)
WebRTC (Voice Chat)
Chart.js (Analytics)
```

### **Backend**
```
Node.js + Express.js
Python (ML/AI Models)
PostgreSQL (Database)
Redis (Cache & Real-time)
Socket.io (Real-time Chat)
```

### **AI/ML**
```
TensorFlow (Mood Prediction)
Natural Language Processing (Chatbot)
Sentiment Analysis
Crisis Detection Models
```

### **Infrastructure**
```
Docker & Docker Compose
Kubernetes (Scaling)
AWS/Google Cloud
Cloudflare (CDN)
```

---

## 📁 Project Structure

```
MindCare-AI/
├── frontend/                 # React.js web application
│   ├── src/
│   │   ├── components/
│   │   │   ├── Chatbot/
│   │   │   ├── MoodTracker/
│   │   │   ├── BreathingExercise/
│   │   │   ├── CrisisAlert/
│   │   │   ├── Analytics/
│   │   │   └── Admin/
│   │   ├── pages/
│   │   ├── hooks/
│   │   ├── utils/
│   │   └── styles/
│   └── package.json
│
├── backend/                  # Node.js API server
│   ├── src/
│   │   ├── routes/
│   │   ├── controllers/
│   │   ├── models/
│   │   ├── middleware/
│   │   ├── services/
│   │   └── config/
│   └── package.json
│
├── ml-models/                # Python ML models
│   ├── mood_prediction/
│   ├── crisis_detection/
│   ├── chatbot/
│   └── sentiment_analysis/
│
├── mobile/                   # React Native mobile app
│   ├── ios/
│   ├── android/
│   └── src/
│
├── database/
│   ├── migrations/
│   ├── seeds/
│   └── schemas/
│
├── docker-compose.yml
├── .env.example
└── README.md
```

---

## 🚀 Quick Start

### **Prerequisites**
- Node.js 16+
- Python 3.9+
- PostgreSQL 13+
- Redis 6+
- Git

### **Installation**

```bash
# Clone repository
git clone https://github.com/Shubham292005/MindCare-AI.git
cd MindCare-AI

# Setup environment
cp .env.example .env

# Install dependencies
npm install
cd frontend && npm install
cd ../backend && npm install

# Start development
docker-compose up -d
npm run dev
```

Application will run at: `http://localhost:3000`

---

## 📞 Emergency Support

### **Crisis Helplines** (India)

| Language | Service | Phone | Website |
|----------|---------|-------|----------|
| **Hindi/English** | AASRA | 9820466726 | aasra.info |
| **English** | iCall | 9152987821 | icallhelpline.org |
| **Hindi** | Vandrevala Foundation | 9999 77 6555 | vandrevalafoundation.org |
| **Tamil** | AIAD | 044 24340060 | aiad.org.in |
| **Telugu** | Telangana Lifeline | 040 27201123 | - |
| **Marathi** | Majlis | 9604-113313 | majlis.org |

---

## 🤝 Contributing

We welcome contributions! Please read [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

**How to contribute:**
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

---

## 📊 Roadmap

### **Phase 1 (Current)**
- [ ] Core chatbot with Hindi support
- [ ] Basic mood tracking
- [ ] Breathing exercises
- [ ] Crisis detection

### **Phase 2**
- [ ] Multi-language support (8+ languages)
- [ ] Voice interface
- [ ] Mood prediction ML
- [ ] Family dashboard

### **Phase 3**
- [ ] Mobile app (iOS/Android)
- [ ] Offline functionality
- [ ] Advanced analytics
- [ ] Integration with helplines

### **Phase 4**
- [ ] Therapist directory
- [ ] Support groups
- [ ] Gamification features
- [ ] Premium features

---

## ⚖️ Important Disclaimers

⚠️ **MindCare-AI is NOT a substitute for professional mental health treatment.**

- No diagnosis or medical advice provided
- For emergencies, always contact local authorities or crisis helplines
- Please consult a licensed therapist for serious mental health concerns
- This is a supportive tool only

---

## 📋 Privacy & Data Protection

- All chats are encrypted end-to-end
- User data is not sold or shared
- GDPR compliant
- Complies with India's Digital Personal Data Protection Act
- Regular security audits
- Clear data retention policies

---

## 📜 License

This project is licensed under the **MIT License** - see [LICENSE](./LICENSE) file for details.

---

## 🙏 Acknowledgments

- Mental health professionals for guidance
- Open-source communities
- Crisis helpline organizations
- Contributors and supporters

---

## 📧 Contact

- **Email**: contact@mindcare-ai.com
- **GitHub**: [@Shubham292005](https://github.com/Shubham292005)
- **Issues**: [GitHub Issues](https://github.com/Shubham292005/MindCare-AI/issues)

---

## 🌍 Supported Languages

- 🇮🇳 **Hindi** (हिंदी)
- 🇮🇳 **Marathi** (मराठी)
- 🇮🇳 **Tamil** (தமிழ்)
- 🇮🇳 **Telugu** (తెలుగు)
- 🇮🇳 **Kannada** (ಕನ್ನಡ)
- 🇮🇳 **Bengali** (বাংলা)
- 🇮🇳 **Punjabi** (ਪੰਜਾਬੀ)
- 🇮🇳 **Gujarati** (ગુજરાતી)
- 🇮🇳 **Urdu** (اردو)
- 🇬🇧 **English**

---

**Made with ❤️ for mental health and wellbeing**

*Together, we can make mental health support accessible to every Indian.*
