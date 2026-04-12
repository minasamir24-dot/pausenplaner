# Pausenplaner - Pharmacy Break Planner

## 1. Project Overview

**Project Name:** Pausenplaner  
**Type:** Single-page web application  
**Core Functionality:** A break scheduling app for pharmacy employees to book 1-hour daily breaks in one of two locations, with conflict prevention and a manager view.  
**Target Users:** Pharmacy employees and manager

---

## 2. UI/UX Specification

### Layout Structure

- **Login Screen:** Centered card with role selection (Employee/Manager) and name input
- **Main App:** Header with user info + logout, calendar section, bookings list
- **Responsive:** Single column, mobile-friendly (min-width: 320px)

### Visual Design

**Color Palette:**
- Primary: `#2E7D32` (Pharmacy green)
- Secondary: `#1565C0` (Blue for manager)
- Background: `#F5F5F5` (Light gray)
- Card: `#FFFFFF` (White)
- Text: `#212121` (Dark gray)
- Accent: `#FFA726` (Orange for kitchen location)
- Accent 2: `#5C6BC0` (Indigo for basement location)
- Error: `#D32F2F` (Red)
- Success: `#388E3C` (Green)

**Typography:**
- Font: System UI, sans-serif
- Headings: 1.5rem - 2rem, bold
- Body: 1rem
- Small: 0.875rem

**Spacing:**
- Card padding: 1.5rem
- Section gap: 1rem
- Element margin: 0.5rem

**Visual Effects:**
- Cards: `box-shadow: 0 2px 8px rgba(0,0,0,0.1)`
- Buttons: Hover brightness adjustment
- Transitions: 0.2s ease for interactions

### Components

1. **Login Card**
   - Role toggle (Mitarbeiter / Leiter)
   - Name input field (required for employees)
   - Login button

2. **Header**
   - Welcome message with user name
   - Role indicator badge
   - Logout button (Abmelden)

3. **Calendar**
   - Month/Year display with navigation arrows
   - Weekday headers (Mo, Di, Mi, Do, Fr, Sa, So)
   - Day grid with booking indicators
   - Click to select day

4. **Booking Panel** (Employee view only)
   - Selected date display
   - Time slot selection (dropdown: 08:00-17:00, hourly)
   - Location selection (radio: Keller / Küche)
   - Book button (Pause buchen)
   - Cancel own break button (if booked)

5. **Bookings List**
   - Table showing: Zeit, Ort, Name
   - Color-coded by location
   - Filtered by selected day

6. **Manager View**
   - Read-only calendar
   - Bookings list only (no booking controls)
   - All employees' breaks visible

---

## 3. Functionality Specification

### Core Features

1. **User Authentication**
   - Employee: Enter name → Main app
   - Manager: Select "Leiter" → Main app (no name needed)
   - Session stored in localStorage

2. **Break Booking (Employees)**
   - Select day → Select time → Select location
   - Validation:
     - Max 2 breaks per time slot (different locations)
     - One break per person per day
   - Success: Show confirmation
   - Error: Show German error message

3. **Calendar Display**
   - Current month shown by default
   - Navigate to previous/next months
   - Days with bookings marked with dot indicator
   - Today highlighted

4. **Day View**
   - Click day to see all bookings for that day
   - Shows: Time, Location (Keller/Küche), Employee name
   - Color-coded by location

5. **Break Cancellation**
   - Employee can cancel their own break on a day
   - Button appears if user has booked that day

6. **Manager View**
   - Full calendar access
   - See all bookings
   - No booking/cancellation buttons

### Data Structure

```javascript
{
  "breaks": [
    { "id": "uuid", "name": "Mitarbeiter Name", "date": "2026-04-12", "time": "09:00", "location": "Keller" }
  ]
}
```

### Edge Cases
- Attempting to book when slot full → Error message
- Attempting to book twice on same day → Error message
- Manager trying to book → Not allowed (no button shown)
- Past dates → Can still view, can still book (if today)

---

## 4. Acceptance Criteria

1. ✅ Login works for employee (name input) and manager (no name)
2. ✅ Calendar displays current month with navigation
3. ✅ Employee can book break with time and location selection
4. ✅ Max 2 breaks per time slot enforced (different locations)
5. ✅ One break per person per day enforced
6. ✅ Bookings displayed in list with time, location, name
7. ✅ Employee can cancel their own break
8. ✅ Manager sees all bookings but cannot book
9. ✅ All UI text in German
10. ✅ Data persists in localStorage