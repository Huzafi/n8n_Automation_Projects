# 🏥 AI Hospital Appointment Assistant — V2

An AI-powered hospital appointment assistant that enables patients to interact naturally through voice, describe their health concerns, find the relevant medical specialty, select an available doctor and appointment slot, and book an appointment automatically.

This project combines **ElevenLabs Voice AI**, **n8n workflow automation**, and **Google Sheets** to create an end-to-end AI-powered appointment scheduling system.

> ⚠️ **Note:** This is a technical prototype / demonstration project. It is not a medical diagnosis system and should not be used as a substitute for professional medical advice.

---

## 🎥 Live Demo

> 🚧 **Live demo video will be added soon.**

**Watch the Full Project Demonstration:**
[▶️ Live Demo Video](#)

---

## ✨ Features

- 🗣️ Natural voice-based patient interaction
- 🩺 AI-powered patient concern routing
- 🏥 Automatic medical specialty selection
- 👨‍⚕️ Doctor retrieval based on specialty
- 📅 Doctor availability checking
- ⏰ Dynamic appointment slot generation
- 🚫 Double-booking prevention
- 📝 Patient information collection
- 🆔 Automatic appointment ID generation
- ⚙️ Automated backend workflows using n8n
- 📊 Google Sheets-based prototype database
- 🔗 API-based communication between ElevenLabs and n8n
- 🔒 Backend validation before appointment creation

---

## 🧠 How It Works

The system follows a structured appointment booking flow:

```text
Patient
   │
   ▼
Voice Conversation
   │
   ▼
ElevenLabs AI Agent
   │
   ▼
Patient describes health concern
   │
   ▼
Route to Medical Specialty
   │
   ▼
Retrieve Available Doctors
   │
   ▼
Patient Selects Doctor
   │
   ▼
Check Doctor Availability
   │
   ▼
Patient Selects Appointment Slot
   │
   ▼
Collect Patient Details
   │
   ▼
Validate Booking Request
   │
   ▼
Check for Existing Booking
   │
   ▼
Generate Appointment ID
   │
   ▼
Save Appointment
   │
   ▼
Booking Confirmation
```

---

## 🏗️ System Architecture

```text
                    ┌──────────────────────┐
                    │       Patient        │
                    │   Voice Conversation │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │     ElevenLabs       │
                    │     Voice Agent      │
                    └──────────┬───────────┘
                               │
                         HTTP Tool Calls
                               │
                               ▼
                    ┌──────────────────────┐
                    │         n8n          │
                    │  Automation Backend  │
                    └──────────┬───────────┘
                               │
          ┌────────────────────┼────────────────────┐
          │                    │                    │
          ▼                    ▼                    ▼
 ┌────────────────┐   ┌────────────────┐   ┌───────────────────┐
 │ Route Patient  │   │  Get Doctors   │   │ Check Availability│
 └────────────────┘   └────────────────┘   └───────────────────┘
          │                    │                    │
          └────────────────────┼────────────────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │   Book Appointment   │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │    Google Sheets     │
                    │   Prototype Database │
                    └──────────────────────┘
```

---

## 🔧 Technology Stack

| Technology | Purpose |
|---|---|
| ElevenLabs | Voice AI and conversational interface |
| n8n | Backend workflow automation |
| Google Sheets | Prototype database |
| Webhooks | Communication between AI agent and backend |
| JavaScript | Data processing and validation inside n8n |
| JSON | API request and response format |

---

## 🤖 AI Agent Tools

The ElevenLabs AI agent uses four backend tools.

### 1. `route_patient`

Routes the patient's stated concern to an appropriate medical specialty.

**Input**

```json
{
  "patient_concern": "stomach pain and acid reflux",
  "specialty_id": "S006"
}
```

**Output**

```json
{
  "success": true,
  "specialty_id": "S006",
  "specialty_name": "Gastroenterology"
}
```

**Purpose**

The workflow uses structured routing data to determine the relevant specialty instead of allowing the AI to invent specialties.

### 2. `get_doctors`

Retrieves active doctors belonging to the selected specialty.

**Input**

```json
{
  "specialty_id": "S006"
}
```

**Example Output**

```json
{
  "success": true,
  "specialty_id": "S006",
  "doctors": [
    {
      "doctor_id": "D006",
      "doctor_name": "Dr. Ayesha Malik",
      "department": "Gastroenterology"
    }
  ]
}
```

### 3. `check_availability`

Checks available appointment slots for a selected doctor and date.

**Input**

```json
{
  "doctor_id": "D006",
  "date": "2026-10-02"
}
```

**Example Output**

```json
{
  "success": true,
  "doctor_id": "D006",
  "date": "2026-10-02",
  "available_slots": [
    "10:00",
    "10:30",
    "11:00",
    "11:30",
    "12:00",
    "12:30",
    "13:00",
    "13:30"
  ]
}
```

The workflow dynamically generates slots based on the doctor's schedule and removes slots that have already been booked.

### 4. `book_appointment`

Creates the final appointment after validating the booking request.

**Required Fields**

- `patient_name`
- `phone_number`
- `specialty_id`
- `doctor_id`
- `date`
- `time`
- `reason`

**Example Request**

```json
{
  "patient_name": "Ali Khan",
  "phone_number": "03001234567",
  "specialty_id": "S006",
  "doctor_id": "D006",
  "date": "2026-10-02",
  "time": "11:30",
  "reason": "Stomach pain and acid reflux"
}
```

**Successful Response**

```json
{
  "success": true,
  "appointment_id": "APT-1790878305793-64E159",
  "message": "Appointment has been successfully booked."
}
```

---

## 🩺 Supported Medical Specialties

The current prototype contains the following specialties:

| ID | Specialty | Description |
|---|---|---|
| S001 | Cardiology | Heart and cardiovascular concerns |
| S002 | Dermatology | Skin, hair and nail concerns |
| S003 | Orthopedics | Bones, joints and muscle concerns |
| S004 | Ophthalmology | Eye-related concerns |
| S005 | ENT | Ear, nose and throat concerns |
| S006 | Gastroenterology | Digestive system and stomach-related concerns |
| S007 | Neurology | Brain, nerve and neurological concerns |
| S008 | General Medicine | General health concerns |

---

## 👨‍⚕️ Doctors

The prototype currently contains sample doctors associated with each specialty.

| Doctor ID | Doctor | Specialty |
|---|---|---|
| D001 | Dr. Ahmed Khan | Cardiology |
| D002 | Dr. Sara Ali | Dermatology |
| D003 | Dr. Usman Raza | Orthopedics |
| D004 | Dr. Hina Ahmed | Ophthalmology |
| D005 | Dr. Bilal Shah | ENT |
| D006 | Dr. Ayesha Malik | Gastroenterology |
| D007 | Dr. Hamza Siddiqui | Neurology |
| D008 | Dr. Fatima Noor | General Medicine |

> These doctors are sample/demo data for this prototype and do not represent real hospital staff.

---

## 📅 Appointment Availability

Doctor availability is stored using the following fields:

- `availability_id`
- `doctor_id`
- `day`
- `start_time`
- `end_time`
- `slot_duration`
- `status`

The current prototype uses a **slot duration of 30 minutes**.

The availability workflow:

1. Receives the requested doctor and date.
2. Converts the date into its weekday.
3. Finds the doctor's working schedule.
4. Generates 30-minute appointment slots.
5. Retrieves existing appointments.
6. Removes already-booked slots.
7. Returns the remaining available slots.

---

## 🔒 Double-Booking Prevention

One of the key features of the system is prevention of duplicate appointments.

Before an appointment is created, the booking workflow checks:

```text
Doctor ID + Appointment Date + Appointment Time
```

If an existing appointment has the same `doctor_id`, `date` and `time`, and its `status` is `booked`, the booking is rejected.

**Example**

```text
Existing Appointment:

Doctor: D006
Date: 2026-10-02
Time: 11:30
Status: booked
```

If another patient tries to book:

```text
Doctor: D006
Date: 2026-10-02
Time: 11:30
```

the system returns:

```json
{
  "success": false,
  "error": "slot_unavailable",
  "message": "The selected appointment slot is no longer available."
}
```

This prevents two patients from being assigned the same appointment slot.

---

## 🆔 Appointment ID Generation

Every successful appointment receives a unique appointment ID.

Example:

```text
APT-1790878305793-64E159
```

The ID is generated automatically by the n8n booking workflow.

---

## 🗄️ Database Structure

The prototype uses Google Sheets as the initial data layer. The spreadsheet contains the following tables/tabs.

### Appointments

Stores booked appointments.

| Field | Description |
|---|---|
| `appointment_id` | Unique appointment identifier |
| `patient_name` | Patient's full name |
| `phone_number` | Patient's phone number |
| `specialty_id` | Selected specialty |
| `doctor_id` | Selected doctor |
| `date` | Appointment date |
| `time` | Appointment time |
| `reason` | Patient's stated reason |
| `status` | Appointment status |

### Specialties

Stores available medical specialties.

- `specialty_id`
- `specialty_name`
- `department`
- `description`

### Doctors

Stores doctors and their specialties.

- `doctor_id`
- `doctor_name`
- `specialty_id`
- `department`
- `status`

### Doctor_Availability

Stores doctor schedules.

- `availability_id`
- `doctor_id`
- `day`
- `start_time`
- `end_time`
- `slot_duration`
- `status`

### Concern_Routing

Stores mappings between common patient concerns and specialties.

- `routing_id`
- `specialty_id`
- `concern_category`
- `examples`
- `status`

Example:

```text
Stomach pain
Acid reflux
Indigestion
Nausea
       ↓
Gastroenterology
```

---

## 🔄 Example End-to-End Conversation

A typical interaction can look like this:

```text
Patient:
I've been having stomach pain and acid reflux.

AI:
Based on your concern, Gastroenterology would be the relevant specialty.

AI:
I found Dr. Ayesha Malik in Gastroenterology.
Would you like to book an appointment with her?

Patient:
Yes.

AI:
What date would you like?

Patient:
October 2nd.

AI:
Let me check the available appointment times.

AI:
The available times are 10:00, 10:30, 11:30 and 12:00.
Which time would you prefer?

Patient:
11:30.

AI:
May I have your full name?

Patient:
Ali Khan.

AI:
And your phone number?

Patient:
03001234567.

AI:
Your appointment has been successfully booked.

Appointment ID:
APT-1790878305793-64E159
```

---

## ⚙️ n8n Workflows

The project contains four backend workflows.

### Hospital - Route Patient

```text
Patient Concern
       ↓
Concern Routing
       ↓
Medical Specialty
```

### Hospital - Get Doctors

```text
Specialty ID
       ↓
Doctors Database
       ↓
Active Doctors
```

### Hospital - Check Availability

```text
Doctor + Date
       ↓
Find Working Day
       ↓
Generate Appointment Slots
       ↓
Read Existing Appointments
       ↓
Remove Booked Slots
       ↓
Return Available Slots
```

### Hospital - Book Appointment

```text
Booking Request
       ↓
Validate Required Fields
       ↓
Check Existing Appointments
       ↓
Prevent Double Booking
       ↓
Generate Appointment ID
       ↓
Append Appointment
       ↓
Return Confirmation
```

---

## 📁 Repository Structure

```text
ai-hospital-appointment-agent/
│
├── n8n/
│   ├── hospital-route-patient.json
│   ├── hospital-get-doctors.json
│   ├── hospital-check-availability.json
│   └── hospital-book-appointment.json
│
├── docs/
│   └── architecture.md
│
├── README.md
├── .gitignore
└── LICENSE
```

---

## 🧪 Testing

The backend workflows were tested individually before connecting the complete system.

Testing included:

- ✅ Patient concern routing
- ✅ Specialty retrieval
- ✅ Doctor retrieval
- ✅ Date-to-weekday conversion
- ✅ Appointment slot generation
- ✅ Availability filtering
- ✅ Successful appointment booking
- ✅ Required-field validation
- ✅ Duplicate booking prevention
- ✅ End-to-end voice agent testing

A duplicate booking test was performed using the same doctor, date and time. The second booking was correctly rejected as unavailable.

---

## 🛡️ Safety & Scope

This project is an appointment scheduling assistant, **not** a medical diagnosis system.

**The AI should:**

- Understand the patient's stated concern.
- Route the concern to an appropriate specialty.
- Retrieve available doctors.
- Check appointment availability.
- Collect required booking information.
- Book the appointment.
- Provide booking confirmation.

**The AI should not:**

- Diagnose medical conditions.
- Prescribe medication.
- Invent doctors.
- Invent appointment slots.
- Provide medical certainty.
- Replace a qualified healthcare professional.

The specialty-routing data used in this prototype is demonstration data and should be reviewed and validated by qualified healthcare professionals before real-world deployment.

---

## 🔐 Security Considerations

Before deploying this system in production, additional security measures should be implemented. These include:

- Secure API credential management
- Environment variables / secrets management
- Authentication for backend endpoints
- Authorization and role-based access
- Protection of patient information
- Secure database access
- HTTPS
- Webhook security
- Logging and monitoring
- Backup and recovery
- Appropriate healthcare privacy and compliance controls

> **Never commit API keys, OAuth tokens, passwords, webhook secrets, or other credentials to GitHub.**

---

## 🚀 Production Roadmap

Potential future improvements include:

- 🗄️ Production database integration
- 👨‍⚕️ Doctor management dashboard
- 🏥 Hospital staff dashboard
- 🔐 Authentication and role-based access
- ❌ Appointment cancellation
- 🔄 Appointment rescheduling
- 📱 SMS notifications
- 💬 WhatsApp integration
- 📧 Email confirmations
- ⏰ Appointment reminders
- 🧑‍🤝‍🧑 Patient profiles
- 📋 Appointment history
- 🏥 Multi-hospital support
- 📊 Analytics dashboard
- 🔌 Hospital Management System integration
- 📅 Calendar integration
- 🛡️ Production-grade security and observability

---

## 🧩 Design Philosophy

The project follows a separation-of-responsibilities approach:

```text
┌─────────────────────────────────────┐
│            ElevenLabs               │
│       Conversation + Voice          │
└──────────────────┬──────────────────┘
                   │
                   ▼
┌─────────────────────────────────────┐
│                n8n                  │
│      Business Logic + Automation    │
└──────────────────┬──────────────────┘
                   │
                   ▼
┌─────────────────────────────────────┐
│          Google Sheets              │
│         Prototype Data Layer        │
└─────────────────────────────────────┘
```

The core principle is:

> **LLM handles conversation and reasoning, while deterministic backend workflows handle business logic and data operations.**

This approach helps make the system more predictable, testable and easier to extend.

---

## 📌 Current Project Status

**V2 Status:** ✅ Functional Prototype

**Completed:**

- [x] Voice AI integration
- [x] Patient concern routing
- [x] Specialty selection
- [x] Doctor retrieval
- [x] Availability checking
- [x] Dynamic slot generation
- [x] Booking validation
- [x] Double-booking prevention
- [x] Appointment ID generation
- [x] Google Sheets integration
- [x] n8n backend workflows
- [x] End-to-end testing

---

## 🎥 Full Project Demonstration

The complete live demonstration video will be added here:

[▶️ Watch the Full AI Hospital Appointment Assistant Demo](#)

---

## 👨‍💻 Author

**Huzaifa Sheikh**

AI / Backend Developer

Focused on:

- Agentic AI
- AI Agents
- Backend Development
- Workflow Automation
- n8n
- OpenAI Agents SDK
- AI Integrations
- FastAPI
- Python

---

## 📄 License

This project is intended for educational, portfolio and demonstration purposes.

See the [LICENSE](LICENSE) file for the applicable license terms.

---

⭐ If you find this project interesting, feel free to explore the workflows and architecture in this repository.
