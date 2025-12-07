# Chat Application Frontend

A modern, real-time chat application built with React, TypeScript, Tailwind CSS, and Socket.IO for seamless messaging and user interaction.

## Features

- **User Authentication:** OTP-based login system
- **Real-time Messaging:** Instant message delivery with Socket.IO
- **User Presence:** See who's online in real-time
- **Typing Indicators:** Know when someone is typing
- **Image Sharing:** Send and receive images in chats
- **Message Status:** Track message delivery and read status
- **Responsive Design:** Works on desktop and mobile devices
- **User Management:** View and search all users
- **Chat Management:** Create and manage multiple conversations

## Prerequisites

- Node.js (v16 or higher)
- npm or yarn
- Backend services running locally (ports 5000, 5001, 5002)

## Installation

### 1. Clone the repository
```bash
git clone <repository-url>
cd frontend
```

### 2. Install dependencies
```bash
npm install
```

## Environment Setup

Create a `.env` file in the root directory with the following variables:

```env
REACT_APP_API_URL=http://localhost:5000
REACT_APP_CHAT_API_URL=http://localhost:5002
REACT_APP_SOCKET_URL=http://localhost:5002
```

## Running the Application

### Development Mode
```bash
npm start
```
The application will open at `http://localhost:3000`

### Build for Production
```bash
npm run build
```

### Run Tests
```bash
npm test
```

## Project Structure

```
frontend/
├── src/
│   ├── components/
│   │   ├── Auth/
│   │   │   ├── Login.tsx
│   │   │   └── OtpVerification.tsx
│   │   ├── Chat/
│   │   │   ├── ChatWindow.tsx
│   │   │   ├── MessageList.tsx
│   │   │   ├── MessageInput.tsx
│   │   │   └── TypingIndicator.tsx
│   │   ├── Users/
│   │   │   ├── UserList.tsx
│   │   │   ├── UserCard.tsx
│   │   │   └── UserSearch.tsx
│   │   ├── Sidebar/
│   │   │   ├── Sidebar.tsx
│   │   │   └── ChatList.tsx
│   │   ├── Common/
│   │   │   ├── Navbar.tsx
│   │   │   ├── Loader.tsx
│   │   │   └── Modal.tsx
│   │   └── Layout/
│   │       └── MainLayout.tsx
│   ├── pages/
│   │   ├── LoginPage.tsx
│   │   ├── ChatPage.tsx
│   │   └── NotFoundPage.tsx
│   ├── services/
│   │   ├── api.ts
│   │   ├── socket.ts
│   │   └── auth.ts
│   ├── context/
│   │   ├── AuthContext.tsx
│   │   └── ChatContext.tsx
│   ├── hooks/
│   │   ├── useAuth.ts
│   │   ├── useChat.ts
│   │   └── useSocket.ts
│   ├── types/
│   │   ├── auth.ts
│   │   ├── chat.ts
│   │   └── user.ts
│   ├── styles/
│   │   └── globals.css
│   ├── App.tsx
│   ├── index.tsx
│   └── index.css
├── public/
│   ├── index.html
│   └── favicon.ico
├── package.json
├── tsconfig.json
├── tailwind.config.js
└── postcss.config.js
```

## Key Components

### Authentication Flow
- **LoginPage:** Email input and OTP request
- **OtpVerification:** OTP verification and token storage
- Protected routes with JWT token validation

### Chat Interface
- **Sidebar:** List of active chats and users
- **ChatWindow:** Main messaging area
- **MessageList:** Displays all messages with timestamps
- **MessageInput:** Text input with image upload capability
- **TypingIndicator:** Shows when user is typing

### User Management
- **UserList:** Browse all available users
- **UserSearch:** Search users by name
- **UserCard:** User profile preview with online status

## Technology Stack

- **Framework:** React 18
- **Language:** TypeScript
- **Styling:** Tailwind CSS
- **State Management:** Context API + Hooks
- **Real-time:** Socket.IO Client
- **HTTP Client:** Axios
- **Routing:** React Router v6
- **Icons:** React Icons
- **Form Handling:** React Hook Form
- **Notifications:** React Toastify

## API Integration

### User Service Integration

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| POST | `/api/v1/login` | Send OTP to email | No |
| POST | `/api/v1/verify` | Verify OTP and get token | No |
| GET | `/api/v1/me` | Get current user profile | Yes |
| GET | `/api/v1/user/all` | Get all users | Yes |
| GET | `/api/v1/user/:id` | Get user by ID | No |
| POST | `/api/v1/update/user` | Update user profile | Yes |

### Chat Service Integration

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| POST | `/api/v1/chat/new` | Create new chat | Yes |
| GET | `/api/v1/chat/all` | Get all chats | Yes |
| POST | `/api/v1/message` | Send message | Yes |
| GET | `/api/v1/message/:chatId` | Get messages by chat | Yes |

## Socket Events Usage

### Emitting Events (Client → Server)
```typescript
socket.emit('typing', { chatId, userId });
socket.emit('stopTyping', { chatId, userId });
socket.emit('joinChat', { chatId });
socket.emit('leaveChat', { chatId });
```

### Listening Events (Server → Client)
```typescript
socket.on('newMessage', (message) => { /* handle */ });
socket.on('messagesSeen', (data) => { /* handle */ });
socket.on('userTyping', (data) => { /* handle */ });
socket.on('userStoppedTyping', (data) => { /* handle */ });
socket.on('getOnlineUser', (users) => { /* handle */ });
```

## Authentication Flow

1. User enters email → OTP sent to email
2. User verifies OTP → JWT token generated
3. Token stored in localStorage
4. Token included in all API requests via Authorization header
5. Socket.IO connection authenticated with token

## State Management

### AuthContext
- Current user information
- Authentication status
- Login/logout functions
- Token management

### ChatContext
- Active chats list
- Current chat messages
- Online users
- Typing status
- Message operations

## Features in Detail

### Real-time Messaging
- Messages appear instantly using Socket.IO
- Message status: sent, delivered, seen
- Timestamps for each message
- User avatars and names

### Image Sharing
- Upload images with messages
- Image preview in chat
- Cloudinary integration for storage
- File size validation

### Typing Indicators
- Shows when user starts typing
- Disappears when user stops
- Smooth animations

### User Presence
- Online/offline status indicators
- Last seen timestamps
- Online users count

## Development Tips

### Environment Variables
Update `.env` file for different backend URLs in development vs. production.

### TypeScript
All components are fully typed. Check `src/types/` for type definitions.

### Hooks
Custom hooks in `src/hooks/` provide reusable logic:
- `useAuth()` - Authentication state and functions
- `useChat()` - Chat state and operations
- `useSocket()` - Socket event handlers

## Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

## Performance Optimization

- Code splitting with React.lazy()
- Image lazy loading
- Memoization of components
- Optimized re-renders
- Message virtualization for large chats

## License

ISC
