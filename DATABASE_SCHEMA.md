# MindCare-AI Database Schema

## Overview
This document outlines the database structure for MindCare-AI mental health platform.

## Tables

### 1. `users`
Core user information

```sql
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email VARCHAR(255) UNIQUE NOT NULL,
  password_hash VARCHAR(255) NOT NULL,
  full_name VARCHAR(255),
  date_of_birth DATE,
  gender VARCHAR(50),
  phone VARCHAR(20),
  user_type ENUM('student', 'professional', 'senior', 'parent') DEFAULT 'student',
  preferred_language VARCHAR(10) DEFAULT 'en',
  avatar_url TEXT,
  bio TEXT,
  is_anonymous BOOLEAN DEFAULT false,
  is_verified BOOLEAN DEFAULT false,
  is_active BOOLEAN DEFAULT true,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  deleted_at TIMESTAMP
);
```

### 2. `moods`
Daily mood tracking records

```sql
CREATE TABLE moods (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  mood_score INT CHECK (mood_score >= 1 AND mood_score <= 10),
  emotion_label VARCHAR(50), -- happy, sad, anxious, calm, etc.
  stress_level INT CHECK (stress_level >= 1 AND stress_level <= 10),
  sleep_hours DECIMAL(4, 2),
  sleep_quality INT CHECK (sleep_quality >= 1 AND sleep_quality <= 5),
  trigger VARCHAR(500), -- what caused the mood
  notes TEXT,
  activities TEXT[], -- exercise, meditation, socializing, etc.
  medication_taken BOOLEAN,
  energy_level INT CHECK (energy_level >= 1 AND energy_level <= 10),
  social_interaction INT CHECK (social_interaction >= 1 AND social_interaction <= 5),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_moods_user_id_created_at ON moods(user_id, created_at DESC);
```

### 3. `chats`
Chatbot conversation records

```sql
CREATE TABLE chats (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  conversation_id UUID NOT NULL, -- groups messages into conversations
  is_anonymous BOOLEAN DEFAULT false,
  language VARCHAR(10) DEFAULT 'en',
  topic VARCHAR(100), -- stress, anxiety, sleep, relationships, etc.
  sentiment_score DECIMAL(3, 2), -- -1 to 1 scale
  crisis_detected BOOLEAN DEFAULT false,
  crisis_severity INT, -- 1-5 scale
  is_encrypted BOOLEAN DEFAULT true,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_chats_user_id ON chats(user_id);
CREATE INDEX idx_chats_conversation_id ON chats(conversation_id);
```

### 4. `messages`
Individual chat messages

```sql
CREATE TABLE messages (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  chat_id UUID NOT NULL REFERENCES chats(id) ON DELETE CASCADE,
  sender_type ENUM('user', 'bot') NOT NULL,
  sender_id UUID REFERENCES users(id),
  content TEXT NOT NULL,
  content_encrypted TEXT, -- encrypted version
  is_read BOOLEAN DEFAULT false,
  reaction VARCHAR(50), -- emoji reaction
  attachments JSONB, -- images, documents, etc.
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_messages_chat_id ON messages(chat_id);
```

### 5. `crisis_alerts`
Crisis detection and response tracking

```sql
CREATE TABLE crisis_alerts (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  severity_level INT CHECK (severity_level >= 1 AND severity_level <= 5),
  alert_type VARCHAR(50), -- self_harm, suicide, abuse, etc.
  detected_content TEXT,
  confidence_score DECIMAL(3, 2),
  is_resolved BOOLEAN DEFAULT false,
  admin_notes TEXT,
  contacted_emergency BOOLEAN DEFAULT false,
  emergency_contact_id UUID REFERENCES users(id),
  helpline_recommended VARCHAR(100),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  resolved_at TIMESTAMP
);

CREATE INDEX idx_crisis_alerts_user_id ON crisis_alerts(user_id);
CREATE INDEX idx_crisis_alerts_is_resolved ON crisis_alerts(is_resolved);
```

### 6. `emergency_contacts`
Parent/guardian emergency contact information

```sql
CREATE TABLE emergency_contacts (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  contact_name VARCHAR(255),
  phone VARCHAR(20),
  email VARCHAR(255),
  relationship VARCHAR(50), -- parent, guardian, sibling, etc.
  is_primary BOOLEAN DEFAULT false,
  notification_threshold INT, -- only alert if crisis severity >= this
  is_notified_on_crisis BOOLEAN DEFAULT true,
  is_active BOOLEAN DEFAULT true,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_emergency_contacts_user_id ON emergency_contacts(user_id);
```

### 7. `breathing_sessions`
Tracking breathing exercise usage

```sql
CREATE TABLE breathing_sessions (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  exercise_type VARCHAR(50), -- box_breathing, 4_7_8, deep_breathing, etc.
  duration_seconds INT,
  cycles_completed INT,
  heart_rate_before INT,
  heart_rate_after INT,
  effectiveness_rating INT CHECK (effectiveness_rating >= 1 AND effectiveness_rating <= 5),
  location VARCHAR(100), -- home, work, school, outdoor, etc.
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_breathing_sessions_user_id ON breathing_sessions(user_id);
```

### 8. `motivation_quotes`
Daily motivation quotes in multiple languages

```sql
CREATE TABLE motivation_quotes (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  english_text TEXT NOT NULL,
  translations JSONB, -- {"hi": "Hindi text", "mr": "Marathi text", ...}
  category VARCHAR(50), -- inspiration, resilience, self_care, etc.
  author VARCHAR(255),
  relevant_moods INT[], -- [sad, anxious, stressed]
  is_active BOOLEAN DEFAULT true,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 9. `meditation_guides`
Guided meditation content

```sql
CREATE TABLE meditation_guides (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  title VARCHAR(255) NOT NULL,
  description TEXT,
  duration_minutes INT,
  language VARCHAR(10),
  audio_url TEXT,
  transcript TEXT,
  difficulty_level VARCHAR(20), -- beginner, intermediate, advanced
  category VARCHAR(50), -- sleep, anxiety, stress, mindfulness, etc.
  instructor_name VARCHAR(255),
  is_active BOOLEAN DEFAULT true,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 10. `meditation_sessions`
User meditation session tracking

```sql
CREATE TABLE meditation_sessions (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  meditation_guide_id UUID NOT NULL REFERENCES meditation_guides(id),
  duration_completed_seconds INT,
  mood_before INT CHECK (mood_before >= 1 AND mood_before <= 10),
  mood_after INT CHECK (mood_after >= 1 AND mood_after <= 10),
  effectiveness_rating INT CHECK (effectiveness_rating >= 1 AND effectiveness_rating <= 5),
  completed BOOLEAN DEFAULT false,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_meditation_sessions_user_id ON meditation_sessions(user_id);
```

### 11. `admin_users`
Admin dashboard users

```sql
CREATE TABLE admin_users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL UNIQUE REFERENCES users(id) ON DELETE CASCADE,
  role VARCHAR(50), -- super_admin, moderator, analyst
  permissions TEXT[],
  is_active BOOLEAN DEFAULT true,
  last_login TIMESTAMP,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 12. `helpline_contacts`
Available helpline numbers

```sql
CREATE TABLE helpline_contacts (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name VARCHAR(255),
  phone VARCHAR(20),
  email VARCHAR(255),
  website VARCHAR(500),
  languages VARCHAR(100)[], -- ["en", "hi", "mr"]
  availability VARCHAR(100), -- 24/7, 9-5, etc.
  specializations VARCHAR(100)[], -- ["suicide", "abuse", "anxiety"]
  region VARCHAR(100),
  country VARCHAR(50) DEFAULT 'India',
  is_active BOOLEAN DEFAULT true,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 13. `user_settings`
User preferences and settings

```sql
CREATE TABLE user_settings (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL UNIQUE REFERENCES users(id) ON DELETE CASCADE,
  preferred_language VARCHAR(10),
  notification_enabled BOOLEAN DEFAULT true,
  email_notifications BOOLEAN DEFAULT true,
  sms_notifications BOOLEAN DEFAULT false,
  push_notifications BOOLEAN DEFAULT true,
  crisis_alert_enabled BOOLEAN DEFAULT true,
  daily_check_in_enabled BOOLEAN DEFAULT true,
  dark_mode BOOLEAN DEFAULT false,
  data_sharing_consent BOOLEAN DEFAULT false,
  anonymous_analytics BOOLEAN DEFAULT true,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 14. `activity_logs`
Audit trail for admin actions

```sql
CREATE TABLE activity_logs (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  admin_id UUID REFERENCES admin_users(id),
  action_type VARCHAR(50),
  resource_type VARCHAR(50),
  resource_id UUID,
  details JSONB,
  ip_address VARCHAR(45),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_activity_logs_admin_id ON activity_logs(admin_id);
CREATE INDEX idx_activity_logs_created_at ON activity_logs(created_at DESC);
```

### 15. `feedback`
User feedback and bug reports

```sql
CREATE TABLE feedback (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id),
  type VARCHAR(50), -- bug, feature_request, general_feedback
  title VARCHAR(255),
  description TEXT,
  rating INT CHECK (rating >= 1 AND rating <= 5),
  attachments JSONB,
  is_resolved BOOLEAN DEFAULT false,
  admin_response TEXT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  resolved_at TIMESTAMP
);

CREATE INDEX idx_feedback_user_id ON feedback(user_id);
CREATE INDEX idx_feedback_is_resolved ON feedback(is_resolved);
```

## Relationships Overview

```
users
├── moods (1:Many)
├── chats (1:Many)
│   └── messages (1:Many)
├── crisis_alerts (1:Many)
├── emergency_contacts (1:Many)
├── breathing_sessions (1:Many)
├── meditation_sessions (1:Many)
├── user_settings (1:1)
└── feedback (1:Many)

admin_users
└── activity_logs (1:Many)

meditation_guides
└── meditation_sessions (1:Many)

helpline_contacts
└── (referenced in crisis_alerts)
```

## Key Indexes for Performance

```sql
-- User lookup
CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_users_user_type ON users(user_type);

-- Quick mood queries
CREATE INDEX idx_moods_user_created ON moods(user_id, created_at DESC);

-- Chat efficiency
CREATE INDEX idx_messages_created ON messages(created_at DESC);

-- Crisis monitoring
CREATE INDEX idx_crisis_severity ON crisis_alerts(severity_level DESC);
```

## Data Retention Policies

- Deleted user data: 30 days (soft delete, then permanent)
- Chat history: 1 year (archived then deleted)
- Logs: 90 days
- Mood data: Indefinite (user can request export/deletion)
- Crisis alerts: Indefinite (legal requirement)

---

**Last Updated**: 2026-05-17
**Version**: 1.0
