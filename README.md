# Gotarsi App Development Prompt

## Part 1: General Information

### App Overview
**Name:** Gotarsi  
**Tagline:** Travel like a local  
**Core Concept:** A map-based social platform connecting travelers with locals for authentic, location-specific advice through direct messaging and optional donations.

### Technical Requirements
- Responsive web application (mobile-first design)
- Interactive map interface with OpenStreetMap
- Real-time chat functionality
- User authentication system
- Database for storing users, tips, and chats
- Payment integration for donations (Stripe/PayPal)
- Clean, minimalist UI with intuitive navigation

### User Types
1. **Local Guides**: Share insider tips about their hometown
2. **Travelers/Explorers**: Discover authentic local recommendations

### Core Features
1. Interactive map with tip pins
2. Tip filtering by category
3. User profiles with metrics
4. Real-time chat system
5. Donation functionality
6. Save tips for later
7. User authentication

## Part 2: UI Development with Dummy Data

### Task
Create a static, responsive web application with the following screens and dummy data:

For Provider independent software: Host on Next.js. 

### Required Screens

#### 1. Landing Page (Map View)
- Full-screen interactive map (OpenStreetMap integration)
- Filter bar with categories: Food & Drink, Viewpoint, Activity, Hidden Gem
- Tip pins displayed on map
- Tip preview cards (bottom sheet style) showing:
  - Guide's profile picture and name
  - Tip content (max 280 characters)
  - "Message" and "Save" buttons

#### 2. Chat Screen
- Standard chat interface with message history
- Guide's name and profile picture in header
- "Say Thanks" donation button (gift icon)
- Donation modal with preset amounts ($2, $5, $10, Custom)
- Message input field with send button

#### 3. Profile Page
- User header: profile picture, name, bio, home city
- Metrics for Guides: "Total Tips Given", "Donations Received"
- Two tabs:
  - My Tips (for Guides): Grid/list of created tips
  - Saved Tips (for Travelers): Grid/list of saved tips
- Active chats list
- Settings icon

### Dummy Data Requirements

#### Places/Tips (10-15 tips)
```
{
  id: string,
  guideName: string,
  guideId: string,
  guideProfilePic: string,
  location: {
    lat: number,
    lng: number,
    city: string,
    country: string
  },
  category: "Food & Drink" | "Viewpoint" | "Activity" | "Hidden Gem",
  title: string,
  content: string (max 280 chars),
  poiName: string,
  createdAt: date
}
```

Include diverse locations like:
- Hidden coffee shops in Prague
- Secret viewpoints in Lisbon
- Local food markets in Bangkok
- Underground music venues in Berlin
- Art galleries in Mexico City

#### Chat Messages (2-3 conversations)
```
{
  conversationId: string,
  participants: [userId, guideId],
  messages: [{
    id: string,
    senderId: string,
    content: string,
    timestamp: date,
    type: "text" | "donation"
  }]
}
```

#### User Profiles (3-5 users)
```
{
  id: string,
  name: string,
  profilePic: string,
  bio: string,
  homeCity: string,
  userType: "guide" | "traveler",
  stats: {
    tipsGiven: number,
    donationsReceived: number,
    savedTips: array
  }
}
```

### Design Requirements
- **Colors**: Clean palette with primary accent color
- **Typography**: Modern, readable fonts
- **Spacing**: Generous whitespace
- **Components**: 
  - Rounded corners
  - Soft shadows
  - Friendly iconography
  - Smooth transitions
- **Responsive**: Mobile-first, works on all devices
- **Accessibility**: Proper contrast ratios, semantic HTML

## Part 3: Full Web App Implementation

### Task
Transform the static UI into a fully functional web application with:

### Backend Requirements

#### Database Schema
1. **Users Table**
   - id, email, password_hash, name, profile_pic, bio, home_city, user_type, created_at

2. **Tips Table**
   - id, user_id, location_lat, location_lng, city, country, category, title, content, poi_name, created_at

3. **Conversations Table**
   - id, traveler_id, guide_id, tip_id, created_at, last_message_at

4. **Messages Table**
   - id, conversation_id, sender_id, content, message_type, created_at

5. **Donations Table**
   - id, sender_id, recipient_id, amount, conversation_id, created_at

6. **Saved_Tips Table**
   - user_id, tip_id, saved_at

#### Authentication System
- User registration with email/password
- Login/logout functionality
- Session management
- Password reset capability
- Protected routes for authenticated users

#### API Endpoints
1. **Auth Routes**
   - POST /auth/register
   - POST /auth/login
   - POST /auth/logout
   - POST /auth/reset-password

2. **User Routes**
   - GET /users/:id
   - PUT /users/:id
   - GET /users/:id/tips
   - GET /users/:id/saved-tips

3. **Tips Routes**
   - GET /tips (with filtering by location/category)
   - POST /tips
   - GET /tips/:id
   - PUT /tips/:id
   - DELETE /tips/:id

4. **Chat Routes**
   - GET /conversations
   - POST /conversations
   - GET /conversations/:id/messages
   - POST /conversations/:id/messages

5. **Donation Routes** (without payment processing)
   - POST /donations (record donation intent)
   - GET /users/:id/donations

#### Real-time Features
- WebSocket connection for live chat
- Message delivery status
- Online/offline user status
- Typing indicators

#### Additional Functionality
1. **Search & Filtering**
   - Filter tips by category
   - Search tips by keyword
   - Location-based tip loading

2. **User Features**
   - Save/unsave tips
   - Edit profile
   - View conversation history
   - Track donation history

3. **Security**
   - Input validation
   - SQL injection prevention
   - XSS protection
   - Rate limiting
   - CORS configuration

4. **Performance**
   - Pagination for tips and messages
   - Lazy loading for map pins
   - Image optimization
   - Caching strategies

### Deployment Considerations
- Environment variables for sensitive data
- Database migrations
- Error logging
- Basic analytics tracking
- Mobile-responsive testing

### Notes
- Do not implement actual payment processing
- Focus on core functionality over advanced features
- Ensure smooth user experience with loading states and error handling
- Include basic form validation
- Add helpful empty states when no data exists
