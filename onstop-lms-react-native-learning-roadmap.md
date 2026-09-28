# OnStop LMS — React Native + Expo Project-Based Learning Plan

## 1. Project Overview

**Project:** OnStop LMS — Student Mobile Application

**Goal:** Build a production-style LMS mobile application from scratch using React Native with Expo and TypeScript while learning mobile architecture, authentication, styling, state management, Expo APIs, real-time communication, location, notifications, testing, performance, and production builds.

### Starting Skill Level

- 3+ years of MERN/full-stack development experience
- Solid React and JavaScript fundamentals
- Recently started working with TypeScript
- Previous React Native/Expo attempts were affected by dependency/versioning and Android Gradle/build issues

### Learning Philosophy

This is a **project-based learning path**, not a theory-only course.

Every milestone follows:

1. Theory
2. Why it exists
3. Small practical example
4. OnStop LMS implementation
5. Testing
6. Common mistakes
7. Production/interview considerations
8. Move to the next milestone

The goal is to understand **why the architecture works**, not just copy implementation code.

---

# 2. Final Product Vision

OnStop LMS will be a student-focused mobile LMS platform.

```text
                    ONSTOP LMS
                         |
        +----------------+----------------+
        |                |                |
      AUTH            COURSES           PROFILE
        |                |
        |                +-- Course
        |                +-- Batch
        |                +-- Modules
        |                +-- Lectures
        |
        +-- Login
        +-- Register
        +-- Refresh Token
        +-- Secure Session

        +---------------------------------+
        |           LEARNING              |
        |                                 |
        | Video Lectures                  |
        | Progress Tracking               |
        | Notes                           |
        | Course Materials                |
        +---------------------------------+

        +---------------------------------+
        |          ATTENDANCE             |
        |                                 |
        | Normal Attendance               |
        | QR Attendance                   |
        | Live Attendance                 |
        | Location Verification           |
        +---------------------------------+

        +---------------------------------+
        |        NOTIFICATIONS            |
        |                                 |
        | Push Notifications              |
        | Deep Linking                    |
        | Course Updates                  |
        | Attendance Alerts               |
        +---------------------------------+
```

---

# 3. Target Architecture

The mobile application will communicate with a backend API.

```text
                    +----------------------+
                    |    Next.js Admin     |
                    |   Optional / Later   |
                    +----------+-----------+
                               |
                               v
+------------------------------------------------------+
|                 OnStop LMS Backend                   |
|                                                      |
| NestJS / REST APIs                                   |
|                                                      |
| Auth | Courses | Batches | Attendance | Notes       |
| Notifications | Users | Purchases | Locations       |
+----------------------------+-------------------------+
                             |
                      REST / WebSocket
                             |
                             v
                 +-------------------------+
                 | React Native + Expo     |
                 |    Student Mobile App   |
                 +-------------------------+
```

### Planned technology stack

#### Mobile

- React Native
- Expo
- TypeScript
- React Navigation / Expo-compatible navigation
- Redux Toolkit
- TanStack Query
- Axios
- Expo APIs
- WebSockets
- EAS Build

#### Backend

Existing or separately developed backend can use:

- NestJS
- TypeScript
- PostgreSQL
- Prisma
- Redis where required
- WebSockets

#### Storage / Media

Depending on the implementation:

- Object storage
- Video storage/streaming
- Mobile local storage
- Secure credential storage

---

# 4. Milestone Roadmap

## Milestone 01 — Environment & Version Discipline

### Objective

Create a clean Expo project and establish a stable development environment before adding application features.

### Topics

- Node.js version management
- npm / pnpm
- Expo CLI
- Expo SDK
- React Native version relationship
- TypeScript configuration
- Android Studio
- Android Emulator
- Expo Go
- Development builds
- EAS Build
- `app.json`
- `app.config.ts`
- Native `android/` and `ios/` directories
- Metro bundler
- Gradle basics
- Android SDK basics
- Environment variables

### Important concepts

```text
Expo Go
   |
   +-- Managed development

Expo Development Build
   |
   +-- Custom native modules

EAS Build
   |
   +-- Cloud Android/iOS builds

Prebuild
   |
   +-- Generate native android/ios projects
```

### First milestone target

```text
Create project
      |
      v
Run Android
      |
      v
Verify TypeScript
      |
      v
Verify navigation foundation
      |
      v
Initialize Git
```

### Rule

Do not install every Expo package at the beginning.

Native capabilities will be introduced one by one to avoid unnecessary dependency and Gradle problems.

---

# Milestone 02 — React Native Foundations

### Objective

Understand what changes when moving from React for the web to React Native.

### Topics

#### Core components

- View
- Text
- Image
- TextInput
- Pressable
- TouchableOpacity
- ScrollView
- FlatList
- SectionList
- SafeAreaView
- KeyboardAvoidingView
- ActivityIndicator
- Modal

### React Native vs Web

```text
React Web                 React Native

<div>                     <View>
<button>                  <Pressable>
<img>                     <Image>
<input>                   <TextInput>
<p>                       <Text>
```

### Important differences

- No traditional CSS files
- Styles are JavaScript/TypeScript objects
- Different CSS property support
- Platform-specific behavior
- Density-independent dimensions
- `Platform`
- `Dimensions`
- `useWindowDimensions`

---

# Milestone 03 — Styling & Flexbox Mastery

### Objective

Become comfortable building mobile UIs without relying blindly on UI libraries.

### Flexbox

Master:

- `flex`
- `flexDirection`
- `justifyContent`
- `alignItems`
- `alignSelf`
- `flexGrow`
- `flexShrink`
- `flexBasis`
- `gap`

Example:

```tsx
<View
  style={{
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  }}
>
```

### Styling topics

- Spacing systems
- Typography
- Colors
- Borders
- Shadows
- Elevation
- Rounded cards
- Responsive layouts
- Percentage dimensions
- Aspect ratios
- Absolute positioning
- zIndex
- Safe areas

### Build a reusable UI kit

```text
OnStop UI Kit

Button
Input
Card
Avatar
Badge
Loader
Header
BottomSheet
Modal
EmptyState
ErrorState
CourseCard
```

---

# Milestone 04 — Navigation Architecture

### Objective

Build scalable mobile navigation instead of putting navigation logic directly into screens.

### Navigation structure

```text
RootNavigator
|
+-- AuthNavigator
|   +-- Login
|   +-- Register
|   +-- ForgotPassword
|
+-- AppNavigator
    |
    +-- Home
    +-- Courses
    +-- Attendance
    +-- Notes
    +-- Profile
```

### Topics

- Stack navigation
- Tab navigation
- Nested navigation
- Dynamic routes
- Route params
- Protected navigation
- Navigation state
- Deep linking

### Example flow

```text
Course List
     |
     v
Course Details
     |
     v
Lecture
     |
     v
Video Player
```

---

# Milestone 05 — Application Architecture

### Objective

Create a maintainable project structure suitable for a production application.

### Proposed structure

```text
src/
|
+-- app/
|
+-- components/
|
+-- screens/
|
+-- navigation/
|
+-- features/
|   +-- auth/
|   +-- courses/
|   +-- attendance/
|   +-- notes/
|   +-- profile/
|   +-- notifications/
|
+-- services/
|   +-- api/
|   +-- storage/
|   +-- notifications/
|
+-- hooks/
|
+-- store/
|
+-- types/
|
+-- utils/
|
+-- constants/
|
+-- assets/
```

### Architectural flow

```text
Screen
  |
  v
Hook / Feature Logic
  |
  v
Service
  |
  v
API
```

Avoid:

```text
Screen
  |
  +-- 1000 lines of business logic
  |
  +-- axios calls
  |
  +-- state management
```

---

# Milestone 06 — API Integration

### Objective

Connect the mobile application with the backend using a clean API layer.

### Topics

- Axios
- API client
- Axios interceptors
- Request handling
- Response handling
- API errors
- Loading states
- Retry
- Timeout
- Pagination
- Caching

### Service architecture

```text
apiClient
    |
    +-- authService
    +-- courseService
    +-- attendanceService
    +-- noteService
    +-- profileService
```

### Request flow

```text
CourseScreen
     |
     v
useCourses()
     |
     v
courseService.getCourses()
     |
     v
apiClient
     |
     v
NestJS API
```

---

# Milestone 07 — Authentication

### Objective

Build a complete production-style mobile authentication flow.

### Features

- Register
- Login
- Logout
- Access token
- Refresh token
- Forgot password
- Reset password
- Session persistence
- Protected routes
- Session restoration

### Authentication architecture

```text
Login
  |
  v
Backend
  |
  +-- Access Token
  +-- Refresh Token
  |
  v
Secure Storage
  |
  v
Auth Provider / Auth Store
  |
  v
Navigation
```

### Storage concepts

Understand the difference between:

- AsyncStorage
- SecureStore
- In-memory state
- HTTP-only cookies
- Persistent sessions

### Important security questions

- Where should access tokens live?
- Where should refresh tokens live?
- What happens when an access token expires?
- How should token refresh be synchronized?
- What happens when refresh fails?
- How should logout clean the local session?

---

# Milestone 08 — State Management

### Objective

Understand the difference between local state, global state, and server state.

### State categories

```text
Local State
    |
    v
Component-level state

Context
    |
    v
Small shared state

Global Client State
    |
    v
Redux Toolkit

Server State
    |
    v
TanStack Query
```

### Planned usage

Redux Toolkit:

```text
auth
user
selected workspace/batch
app preferences
```

TanStack Query:

```text
courses
lectures
attendance
notes
notifications
```

### Important principle

```text
Redux != API cache
```

The goal is to understand why server state should not automatically be treated as global client state.

---

# Milestone 09 — LMS Course Module

### Objective

Build the core LMS experience.

### Home screen

```text
Welcome User

Continue Learning
Upcoming Classes
Attendance
Notifications

My Courses
```

### Course hierarchy

```text
Course
  |
  v
Batch
  |
  v
Modules
  |
  v
Lessons
  |
  v
Video
```

### Enrollment isolation

```text
User
  |
  v
Enrollment
  |
  v
Course
  |
  v
Batch
  |
  v
Lectures
```

This module will also teach authorization and data isolation concepts.

---

# Milestone 10 — Video Lectures

### Objective

Implement a practical mobile video-learning experience.

### Flow

```text
Course
  |
  v
Lecture
  |
  v
Video Player
```

### Topics

- Video playback
- Playback controls
- Buffering
- Fullscreen
- Orientation
- Playback progress
- Resume position
- Network failure
- Video streaming considerations

### Progress tracking

```text
Student watches lecture
        |
        v
Progress = 70%
        |
        v
Backend
        |
        v
Saved progress
```

---

# Milestone 11 — Notes System

### Objective

Build lecture-specific notes with local and server state considerations.

### Features

- Create note
- Edit note
- Delete note
- Search notes
- Lecture-specific notes
- Timestamped notes
- Offline drafts

### Topics

- Keyboard handling
- Forms
- Validation
- Local persistence
- Optimistic updates
- Server synchronization

### Flow

```text
Course
  |
  v
Lecture
  |
  v
Notes
```

---

# Milestone 12 — Expo Image Gallery / Media

### Objective

Learn how mobile media selection differs from web file inputs.

### Use cases

- Profile picture
- Assignment submission
- Course material
- Student documents

### Topics

- Permissions
- Media picker
- URI handling
- File metadata
- Upload
- Image compression
- Preview
- Error handling

### Flow

```text
Gallery
   |
   v
Select Image
   |
   v
Preview
   |
   v
Upload
   |
   v
Backend / Object Storage
```

---

# Milestone 13 — Camera

### Objective

Use the device camera for LMS functionality.

### Use cases

- Profile verification
- QR attendance
- Document capture
- Barcode/QR scanning

### Topics

- Camera permissions
- Camera lifecycle
- Camera preview
- QR/barcode scanning
- Camera errors
- Platform differences

### Attendance example

```text
Teacher generates QR
        |
        v
Student opens camera
        |
        v
Scan QR
        |
        v
Backend validates
        |
        v
Attendance recorded
```

---

# Milestone 14 — File System

### Objective

Work with files stored locally on the device.

### Use cases

- Download notes
- Download PDFs
- Course materials
- Offline files

### Topics

- File URI
- Directories
- Read/write
- Download
- Delete
- Cache
- Storage permissions
- File cleanup

---

# Milestone 15 — Audio

### Objective

Learn mobile audio playback and recording.

### Use cases

- Audio lectures
- Voice notes
- Audio explanations

### Topics

- Play
- Pause
- Seek
- Duration
- Progress
- Record
- Permissions
- Audio lifecycle
- Background behavior

---

# Milestone 16 — Attendance System

### Objective

Build a complete LMS attendance system.

### Basic attendance

```text
Student
  |
  v
Batch
  |
  v
Today's Class
  |
  v
Attendance
```

### QR attendance

```text
Teacher generates QR
        |
        v
Student scans QR
        |
        v
Backend validation
        |
        v
Attendance recorded
```

### Live attendance

```text
Student App
     |
     | WebSocket
     v
NestJS Gateway
     |
     v
Attendance Service
     |
     v
PostgreSQL
```

### Topics

- Attendance states
- Duplicate prevention
- Session validation
- Time windows
- QR validation
- WebSockets
- Real-time UI updates
- Failure handling

---

# Milestone 17 — Location Tracking

### Objective

Use device location for attendance and location-aware features.

### Use cases

- Attendance verification
- Class location
- Campus tracking
- Live attendance
- Geofencing

### Topics

- Foreground location
- Background location
- Permissions
- GPS coordinates
- Distance calculation
- Geofencing
- Battery implications
- Privacy considerations

### Example

```text
Student Location
       |
       v
Calculate Distance
       |
       v
Class Location
       |
       v
Within Allowed Radius?
       |
     +---+---+
     |       |
    YES      NO
     |       |
     v       v
Allow     Reject
Attendance Attendance
```

Continuous location tracking should be used only when the product requirement justifies its battery and privacy costs.

---

# Milestone 18 — Push Notifications

### Objective

Build a complete notification pipeline.

### Use cases

- Course announcements
- Attendance reminders
- New lecture notifications
- Assignment reminders
- Batch announcements

### Architecture

```text
Backend
   |
   v
Notification Service
   |
   v
Push Provider
   |
   v
Expo Notifications
   |
   v
Mobile Device
```

### Topics

- Device push token
- Notification permissions
- Foreground notifications
- Background notifications
- Notification tap
- Deep linking
- Notification preferences
- Token refresh

### Example

```text
"New React Lecture"

       |
       v
User taps notification
       |
       v
Notification handler
       |
       v
Course
       |
       v
Lecture
```

---

# Milestone 19 — Offline-First Features

### Objective

Make selected LMS features useful even with unreliable connectivity.

### Offline features

- Notes
- Recently viewed courses
- Lecture progress
- Basic profile
- Drafts

### Topics

- Network detection
- Local persistence
- Sync queues
- Conflict handling
- Optimistic updates
- Retry strategies
- Offline/online transitions

### Architecture

```text
                 +-- API
                 |
UI --> Repository
                 |
                 +-- Local Storage
```

---

# Milestone 20 — Performance Optimization

### Objective

Understand and optimize React Native performance instead of blindly applying memoization.

### Rendering

- `React.memo`
- `useMemo`
- `useCallback`
- Component boundaries
- Avoiding unnecessary renders

### Lists

- `FlatList`
- `keyExtractor`
- `getItemLayout`
- `windowSize`
- `initialNumToRender`
- Large lists
- Pagination

### Images

- Image caching
- Compression
- Correct dimensions
- Lazy loading
- Memory considerations

### Network

- Pagination
- Caching
- Request deduplication
- Prefetching

### Mobile-specific performance

- JS thread
- UI thread
- JSI concepts
- Animation performance
- Memory
- Battery
- Native modules

---

# Milestone 21 — Testing

### Objective

Test the mobile application at multiple levels.

## Unit testing

Test:

- Utilities
- Hooks
- Services
- Reducers
- Business logic

## Integration testing

Test:

- Login
- Course fetching
- Attendance
- Notes
- Profile
- Notifications

## End-to-end testing

Primary flow:

```text
Register
   |
   v
Login
   |
   v
Select Course
   |
   v
Watch Lecture
   |
   v
Take Notes
   |
   v
Mark Attendance
   |
   v
Receive Notification
```

---

# Milestone 22 — Production Build & Release

### Objective

Learn how to build and release the application without blindly modifying Gradle files.

### Build lifecycle

```text
Development
    |
    v
Development Build
    |
    v
Preview Build
    |
    v
Production Build
```

### Topics

- EAS
- Android APK
- Android AAB
- iOS builds
- App signing
- Android keystore
- Credentials
- Environment variables
- App version
- Build number
- OTA updates
- Build profiles
- Release channels
- Native configuration
- Gradle troubleshooting

### Core debugging principle

When a build fails:

```text
Read error
   |
   v
Identify package/version involved
   |
   v
Check Expo SDK compatibility
   |
   v
Check native dependency compatibility
   |
   v
Clean/rebuild only when justified
   |
   v
Change versions intentionally
```

Do not randomly upgrade/downgrade packages.

---

# 5. MVP Feature Set

The MVP should contain:

```text
Authentication
    |
    +-- Register
    +-- Login
    +-- Logout
    +-- Refresh Token
    +-- Session Persistence

LMS
    |
    +-- Courses
    +-- Batches
    +-- Modules
    +-- Lectures
    +-- Video Playback
    +-- Progress Tracking

Student
    |
    +-- Profile
    +-- Student Information
    +-- Course Enrollment

Attendance
    |
    +-- Normal Attendance
    +-- QR Attendance
    +-- Live Attendance
    +-- Location Verification

Notes
    |
    +-- Create
    +-- Edit
    +-- Delete
    +-- Search
    +-- Offline Draft

Notifications
    |
    +-- Push Notifications
    +-- Deep Linking
    +-- Course Updates
    +-- Attendance Alerts

Device APIs
    |
    +-- Gallery
    +-- Camera
    +-- Files
    +-- Audio
    +-- Location
```

---

# 6. V2 / Nice-to-Have Features

These should be implemented only after the MVP is stable.

## Payment Integration

```text
Course
   |
   v
Checkout
   |
   v
Payment Gateway
   |
   v
Webhook
   |
   v
Enrollment
```

Topics:

- Payment SDK
- Payment lifecycle
- Webhooks
- Payment verification
- Failed payments
- Refund handling
- Idempotency

---

## Chat

```text
Student <----> Teacher
      |
      +----> Batch
```

Possible technologies:

- WebSockets
- Socket.IO
- Push notifications
- Message persistence

Topics:

- Online/offline status
- Typing indicators
- Read receipts
- Message pagination
- Delivery status
- Offline messages

---

## Video Calling

```text
Student <-----> Teacher
```

Topics:

- WebRTC concepts
- Signaling
- STUN/TURN
- Media permissions
- Call lifecycle
- Network changes
- Video/audio state

For the project, prefer a dedicated video provider initially instead of building the entire infrastructure from scratch.

---

## AI-Based Tests & Analysis

```text
Course
   |
   v
AI Test
   |
   v
Questions
   |
   v
Student Answers
   |
   v
Evaluation
   |
   v
Performance Analysis
   |
   v
Personalized Recommendations
```

Possible AI capabilities:

- Question generation
- MCQ generation
- Answer evaluation
- Weak-topic detection
- Learning recommendations
- Personalized tests
- Performance summaries

---

# 7. Complete Learning Sequence

The complete roadmap is:

```text
01. Environment & Expo
        |
        v
02. React Native Fundamentals
        |
        v
03. Flexbox & Styling
        |
        v
04. Reusable Components
        |
        v
05. Navigation
        |
        v
06. Application Architecture
        |
        v
07. API Integration
        |
        v
08. Authentication
        |
        v
09. State Management
        |
        v
10. LMS Courses
        |
        v
11. Video Lectures
        |
        v
12. Notes
        |
        v
13. Image Gallery
        |
        v
14. Camera
        |
        v
15. File System
        |
        v
16. Audio
        |
        v
17. Attendance
        |
        v
18. WebSockets / Live Attendance
        |
        v
19. Location
        |
        v
20. Push Notifications
        |
        v
21. Offline Support
        |
        v
22. Performance
        |
        v
23. Testing
        |
        v
24. EAS / APK / Production
        |
        v
25. V2 Features
        |
        +-- Payments
        +-- Chat
        +-- Video Calling
        +-- AI Tests & Analysis
```

---

# 8. Definition of Done

The project is considered successful when the following are true:

### Development

- [ ] Expo project is stable
- [ ] Android development works
- [ ] TypeScript is configured
- [ ] Project architecture is understood
- [ ] Navigation is understood
- [ ] Styling system is understood

### Authentication

- [ ] Register works
- [ ] Login works
- [ ] Access token works
- [ ] Refresh token works
- [ ] Secure session persistence works
- [ ] Logout works
- [ ] Protected routes work

### LMS

- [ ] Courses load
- [ ] Batches are isolated
- [ ] Course details work
- [ ] Lectures work
- [ ] Video playback works
- [ ] Progress is persisted
- [ ] Student information works

### Device APIs

- [ ] Gallery works
- [ ] Camera works
- [ ] QR scanning works
- [ ] File operations work
- [ ] Audio works
- [ ] Location works

### Attendance

- [ ] Attendance can be marked
- [ ] Duplicate attendance is prevented
- [ ] QR attendance works
- [ ] Live attendance works
- [ ] Location verification works

### Notifications

- [ ] Push permission works
- [ ] Device token registration works
- [ ] Push notification works
- [ ] Notification tap works
- [ ] Deep linking works

### Offline

- [ ] Offline notes work
- [ ] Drafts persist
- [ ] Sync works
- [ ] Retry works

### Quality

- [ ] Unit tests exist
- [ ] Integration tests exist
- [ ] Main E2E flow works
- [ ] Performance issues have been checked
- [ ] Error handling exists
- [ ] Loading states exist
- [ ] Empty states exist
- [ ] Network failure states exist

### Production

- [ ] Development build works
- [ ] Preview build works
- [ ] APK can be generated
- [ ] AAB can be generated
- [ ] Environment variables are configured
- [ ] Signing/credentials are understood
- [ ] Production build works
- [ ] Release process is documented

---

# 9. Learning Rules

## Rule 1 — Do not skip fundamentals

Even with React experience, React Native introduces:

- Mobile lifecycle
- Native permissions
- Device APIs
- Native builds
- Android/iOS differences
- App state
- Offline behavior
- Battery constraints

These need dedicated learning.

## Rule 2 — One feature at a time

Avoid installing everything upfront.

Bad approach:

```text
Expo
+ Camera
+ Location
+ Notifications
+ Audio
+ Video
+ Maps
+ Payments
+ WebSockets
+ Native modules
```

Better approach:

```text
Core Expo
   |
   v
Navigation
   |
   v
API
   |
   v
Auth
   |
   v
Course
   |
   v
Device API
   |
   v
Real-time
```

## Rule 3 — Understand the dependency tree

Before installing a package, understand:

```text
Expo SDK
   |
   v
React Native version
   |
   v
Native dependency
   |
   v
Android/iOS compatibility
```

## Rule 4 — Do not blindly fix Gradle

Gradle errors are often symptoms of:

- incompatible native dependency
- wrong Android SDK
- incompatible React Native version
- incompatible Expo SDK
- Java version mismatch
- Kotlin version mismatch
- Gradle plugin mismatch

We will diagnose the root cause rather than repeatedly changing versions.

## Rule 5 — Build like a production application

Every major feature should consider:

```text
Loading
Success
Empty
Error
Offline
Unauthorized
Retry
```

---

# 10. Expected Outcome

After completing this roadmap, the goal is not simply:

> "I know React Native."

The goal is:

> "I can design, build, debug, test, optimize, and release a production React Native application using Expo."

You should be able to explain:

- How React Native differs from React web
- How Expo works
- How navigation is structured
- How authentication works on mobile
- How secure storage works
- How state management should be separated
- How server state differs from client state
- How mobile permissions work
- How camera/gallery/files/audio/location APIs work
- How push notifications work
- How WebSockets work on mobile
- How offline synchronization works
- How to optimize lists and rendering
- How Android builds work
- Why Gradle errors happen
- How EAS builds work
- How to generate APK/AAB
- How to troubleshoot production builds

---

# 11. Starting Point

The first implementation milestone is:

**Milestone 01 — Environment & Version Discipline**

Initial target:

```text
Create OnStop LMS
       |
       v
Verify Expo environment
       |
       v
Verify Android emulator/device
       |
       v
Verify TypeScript
       |
       v
Create clean Git repository
       |
       v
Create initial project architecture
       |
       v
Run a clean development build
```

Only after this foundation is stable should we start building the LMS features.

---

## Project Principle

**Learn the platform while building the product.**

Every new React Native concept should have a real purpose inside OnStop LMS, so that the final application becomes both a working portfolio project and a practical React Native learning system.
