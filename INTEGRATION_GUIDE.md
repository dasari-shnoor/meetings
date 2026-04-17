# Shnoor Meetings: Feature Integration Guide

This folder contains the complete code for the **Meeting Room (WebRTC)** and the **AI Chatbot (Home Page)** features. Follow these steps to integrate them into your project.

---

## 1. Prerequisites (Dependencies)

Ensure you have the following packages installed in your projects:

### Frontend (React/Vite)
```bash
npm install lucide-react react-router-dom
```

### Backend (FastAPI/Python)
```bash
pip install fastapi uvicorn python-dotenv pydantic
```

---

## 2. Frontend Integration

### A. Directory Structure
Merge the `frontend/src` folder with your existing `src` folder. 
- **Components**: `src/components/` (ChatbotPanel, MeetingHeader, etc.)
- **Pages**: `src/pages/` (LandingPage, MeetingRoom)
- **Hooks**: `src/hooks/` (useWebRTC.js)

### B. Routing Setup (`App.jsx`)
Update your `App.jsx` to include the following routes:

```javascript
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';
import LandingPage from './pages/LandingPage';
import MeetingRoom from './pages/MeetingRoom';

function App() {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<LandingPage />} />
        <Route path="/room/:id" element={<MeetingRoom />} />
      </Routes>
    </Router>
  );
}
```

### C. Styling (`index.css`)
Add the chatbot bounce animation to your `index.css`:

```css
@keyframes bounce-short {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-10%); }
}
.animate-bounce-short {
  animation: bounce-short 2s ease-in-out infinite;
}
```

---

## 3. Backend Integration

### A. Directory Structure
Merge the `backend/` folder:
- **Routers**: `routers/meeting.py`, `routers/signaling.py`
- **Core**: `core/database.py`

### B. Main API Setup (`main.py`)
Include the new routers in your `main.py`:

```python
from fastapi import FastAPI
from routers import meeting, signaling

app = FastAPI()

# Include routers
app.include_router(meeting.router)
app.include_router(signaling.router)

# WebSocket signaling endpoint is handled in signaling.py
```

### C. Environment Variables (`.env`)
I have included a template `.env` file in the `backend/` folder. Ensure it is located in the root of your backend directory:

```env
PORT=8000
DATABASE_URL=shnoor_meetings.db
```

---

## 4. How to Use

1. **Start Backend**: `python main.py`
2. **Start Frontend**: `npm run dev`
3. **Landing Page**: You will see a floating **Bot Icon** in the bottom right. Click it to open the AI Assistant.
4. **Meeting**: Click "New Meeting" to create a room. Sharing the link with others will allow them to join via WebRTC.

---

## Tips for Antigravity
If you are using **Antigravity** to help with the integration, you can simply tell it:
*"I have a folder 'shnoor_feature_export'. Please help me integrate the frontend and backend files into my current workspace according to the INTEGRATION_GUIDE.md."*
