# Quiz Application

A full-stack quiz application built with the MERN stack (MongoDB-less version using React, Express, and Node.js).

## 🎯 Features

### Core Functionality

- **Email Collection**: Start page with email validation
- **15 Questions**: Fetched from OpenTDB API
- **30-Minute Timer**: Countdown timer with auto-submit functionality
- **Question Navigation**: Navigate between questions freely
- **Visual Indicators**: Track visited and attempted questions
- **Results Report**: Detailed comparison of user answers vs correct answers

### Technical Implementation

- **Frontend**: React.js with hooks and modern ES6+ syntax
- **Backend**: Express.js server for API proxy
- **Responsive Design**: Mobile-friendly interface
- **Browser Compatible**: Works on Chrome, Firefox, Safari, and Edge

## 📁 Project Structure

```
quiz-app/
├── client/ # React frontend
│ ├── public/
│ │ └── index.html
│ ├── src/
│ │ ├── components/
│ │ │ ├── StartPage.jsx
│ │ │ ├── QuizPage.jsx
│ │ │ ├── QuestionNav.jsx
│ │ │ ├── Timer.jsx
│ │ │ └── ReportPage.jsx
│ │ ├── App.js
│ │ ├── App.css
│ │ ├── index.js
│ │ └── index.css
│ └── package.json
├── server/ # Express backend
│ ├── server.js
│ └── package.json
└── README.md
```

## 🚀 Installation & Setup

### Prerequisites

- Node.js (v14 or higher)
- npm or yarn

### Backend Setup

1. Navigate to the server directory:

```
   cd server
```

2. Install dependencies:

```
   npm install
```

3. Start the server:

```
   npm start
```

The server will run on `http://localhost:5000`

### Frontend Setup

1. Open a new terminal and navigate to the client directory:

```
   cd client
```

2. Install dependencies:

```
   npm install
```

3. Start the React application:

```
   npm start
```

The application will open in your browser at `http://localhost:3000`

## 🌐 Deployment

### Backend

- **Platform**: Render
- **URL**: https://quiz-app-backend3.onrender.com

### Frontend

- **Platform**: Vercel
- **URL**: https://quiz-app-frontend-gy6fas7ta-khushi-rastogis-projects-5e58af8c.vercel.app/

## 🎮 How to Use

1. **Start Page**: Enter your email address and click "Start Quiz"
2. **Quiz Page**:
   - Answer questions by clicking on options
   - Use Previous/Next buttons to navigate
   - Use the question overview panel to jump to any question
   - Monitor the timer at the top
   - Submit when ready or wait for auto-submit
3. **Report Page**: Review your answers and see the correct answers

## 🏗️ Technical Approach

### Problem-Solving Strategy

1. **API Integration**: Used Express backend to proxy OpenTDB API requests to avoid CORS issues
2. **State Management**: Utilized React hooks (useState, useEffect) for managing application state
3. **Timer Logic**: Implemented countdown with auto-submit using useEffect cleanup
4. **Question Tracking**: Used Set data structure to efficiently track visited questions
5. **Answer Storage**: Object-based storage for O(1) answer lookup and updates

### Components Built

#### StartPage

- Email validation with regex
- API call to fetch questions
- Loading and error states

#### QuizPage

- Main quiz interface
- Answer selection and storage
- Navigation logic

#### Timer

- Countdown from 30 minutes
- Warning state for last 5 minutes
- Auto-submit trigger

#### QuestionNav

- Visual overview of all questions
- Status indicators (current, attempted, visited, not-visited)
- Click-to-navigate functionality

#### ReportPage

- Score calculation
- Side-by-side answer comparison
- Color-coded correct/incorrect answers

## 📝 API Endpoints

### Backend API

- `GET /api/health` - Health check
- `GET /api/questions` - Fetch 15 random quiz questions
- `GET /` - API information

## 🎨 Design Features

- Animated gradient background
- Glassmorphism UI elements
- Smooth transitions and hover effects
- Mobile-responsive design
- Custom scrollbars
- Color-coded question navigation

## 👤 Author

**Khushi Rastogi**

- GitHub: [@15khushirastogi](https://github.com/15khushirastogi)

## 🚧 Challenges Faced & Solutions

### Challenge 1: Cross-Origin Resource Sharing (CORS) Policy Violations

**Problem**: Direct API calls from the React frontend to the Open Trivia Database API were blocked by browser CORS policy, preventing questions from loading.

**Solution**: Implemented a Node.js/Express backend server as a reverse proxy to handle API requests. The backend fetches data from OpenTDB API server-side (where CORS doesn't apply) and forwards it to the frontend with proper CORS headers enabled using the cors middleware.

### Challenge 2: HTML Entity Encoding in API Responses

**Problem**: Questions and answers returned from the OpenTDB API contained HTML entities (e.g., &quot;, &#039;, &amp;) that displayed incorrectly in the UI.

**Solution**: Created a decodeHTML utility function that uses the browser's native DOMParser or textarea element to automatically decode HTML entities into readable text, ensuring proper display of special characters.

### Challenge 3: Randomizing Answer Order

**Problem**: The correct answer was always in a predictable position since the API returns it separately from incorrect answers, making quizzes too easy.

**Solution**: Combined the correct_answer and incorrect_answers arrays into a single choices array, then shuffled using array.sort(() => Math.random() - 0.5) to randomize answer positions for each question.

### Challenge 4: Timer Auto-Submission Mechanism

**Problem**: Needed to automatically submit the quiz when the 30-minute timer reached zero, even if the user hadn't clicked submit.

**Solution**: Implemented a useEffect hook that monitors the timeUp state variable. When the timer reaches zero, it sets timeUp to true, triggering the effect to automatically call the submission function and redirect to the results page.

## 📦 Dependencies

### Backend

- express: ^4.18.2
- cors: ^2.8.5
- axios: ^1.6.0

### Frontend

- react: ^18.2.0
- react-dom: ^18.2.0
- axios: ^1.6.0
