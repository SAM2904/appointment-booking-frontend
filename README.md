# # Simple Appointment Booking System UI

A simple appointment booking web ui system developing with Vue 3 in Vite targets only for the user can book the timeslots for services and for admin, he can save his working hours according to weekday.

* Note: Before setup this project, Please setup the laravel backend project. **Backend Project GitHub Repo:** (https://github.com/SAM2904/appointment-booking-backend) *

# Features

## Client
On homepage, there is Datepicker for selecting booking date. After select the date, the available timeslots are displayed. When user choose the suitable timeslot, then he can able to book the appointment by entering his email.
* Flow
1. Select a date
2. View available time slots
3. Select a slot
4. Enter email
5. Book appointment

## Admin
No Login Required.
On the homepage, there is a button on top shows "Admin Working Hours". After click on it, you see the option for Add working hour rules & view the list of saved working hour rules.
* Flow
1. Switch to Admin mode
2. Add working hours
3. View list working hours

## API Integration 
This Vue Js project communicates with the Laravel APIs using Axios. **Backend project Github repo:** (https://github.com/SAM2904/appointment-booking-backend). The backend is treated as the single source of availability and booking validation.

# Notes
 - State is managed locally.
 - No routing is used as the app is small.
 - UI is intentionally minimal to focus on functionality.

## Tech Stack & Pre-requisites 

- Vue 3 (Options API)
- Vite
- Axios
- HTML / CSS 
- npm(must be installed on your system)

## Project Setup

  First clone the project using git clone command.
  After cloned the project, open the folder where you cloned the project and then run below commands.

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```



## Frontend File Structure
appointment-booking-frontend/

├── src/

│   ├── components/

│   │   ├── DatePicker.vue

│   │   ├── TimeSlots.vue

│   │   ├── BookingForm.vue

│   │   └── AdminWorkingHours.vue

│   ├── App.vue

│   └── main.js

├── package.json

├── vite.config.js

└── README.md

---

## Component Responsibilities

### `App.vue`
Root component.

- Controls Client/Admin mode switching
- Manages shared state:
  - Selected date
  - Available slots
  - Selected slot
- Handles API communication

---

### `DatePicker.vue`
- Provides date selection UI
- Emits selected date using a custom event
- Prevents past date selection

---

### `TimeSlots.vue`
- Displays available slots returned by backend
- Emits selected slot to parent component
- Does not contain business logic

---

### `BookingForm.vue`
- Allows user to enter email
- Sends booking request to backend
- Displays booking success or error messages

---

### `AdminWorkingHours.vue`
- Allows admin to:
  - Add working hour rules
  - View existing rules
- Uses admin APIs (no authentication as per assignment)

---
