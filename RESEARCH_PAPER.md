# Blockchain Healthcare DApp: A Decentralized Medical Management System

## Research Paper & Complete Project Documentation

---

## Table of Contents

1. [Executive Summary](#executive-summary)
2. [Introduction](#introduction)
3. [Project Overview](#project-overview)
4. [Tech Stack & Architecture](#tech-stack--architecture)
5. [System Architecture](#system-architecture)
6. [Smart Contract Design](#smart-contract-design)
7. [Database & Data Management](#database--data-management)
8. [Frontend Implementation](#frontend-implementation)
9. [Key Features & Functionality](#key-features--functionality)
10. [Security & Efficiency](#security--efficiency)
11. [Installation & Setup](#installation--setup)
12. [Deployment Guide](#deployment-guide)
13. [Running the Application](#running-the-application)
14. [API & Contract Functions](#api--contract-functions)
15. [Conclusion](#conclusion)

---

## Executive Summary

The Blockchain Healthcare DApp is a decentralized application that leverages blockchain technology to manage medical records, doctor appointments, medicine prescriptions, and patient-doctor interactions. Built with Solidity smart contracts and a modern Web3 frontend using Next.js, this system ensures data immutability, transparency, and security while maintaining user privacy. The application supports multiple user roles (Patients, Doctors, and Administrators) with role-based access control and integrates IPFS for decentralized file storage.

---

## Introduction

### Problem Statement

Traditional healthcare systems face several critical challenges:
- **Centralized Data Vulnerability**: Patient records stored in centralized servers are prone to breaches
- **Data Fragmentation**: Medical records scattered across multiple providers
- **Lack of Transparency**: Patients cannot verify doctor credentials or treatment history
- **Inefficient Appointment System**: Manual scheduling and coordination is time-consuming
- **Prescription Fraud**: No way to verify authentic prescriptions from authorized doctors
- **High Administrative Costs**: Intermediaries increase overall system costs

### Solution

Our Blockchain Healthcare DApp addresses these issues by:
- **Immutable Records**: Patient data stored on blockchain cannot be altered or deleted
- **Decentralized Storage**: Using IPFS for distributed file storage
- **Smart Contracts**: Automated verification and execution of healthcare transactions
- **Transparent Doctor Verification**: On-chain doctor registration and approval system
- **Secure Messaging**: End-to-end encrypted chat between patients and doctors
- **Medication Management**: Track medicines from registration to purchase

---

## Project Overview

### Vision

Create a transparent, secure, and efficient healthcare ecosystem where:
- Patients own and control their medical records
- Doctors are verified and accountable
- All transactions are immutable and auditable
- Administrative overhead is minimized through automation

### Scope

The DApp includes:
1. **Patient Management**: Registration, profile, medical history, appointments
2. **Doctor Management**: Registration, approval, appointment scheduling, treatment records
3. **Medicine Management**: Inventory, prescriptions, orders, discounts
4. **Appointment System**: Booking, tracking, completion, history
5. **Communication**: Direct messaging between patients and doctors
6. **Admin Dashboard**: Analytics, user management, fee management
7. **Notification System**: Real-time event notifications

---

## Tech Stack & Architecture

### Frontend Technology Stack

| Technology | Version | Purpose |
|-----------|---------|---------|
| **Next.js** | 13.4.19 | React framework for SSR and static generation |
| **React** | 18.2.0 | Core UI library |
| **Tailwind CSS** | 3.3.1 | Utility-first CSS framework for styling |
| **React Query** | 5.59.0 | Server state management and caching |
| **Wagmi** | 2.12.17 | React hooks for Ethereum interactions |
| **Viem** | 2.21.19 | TypeScript Ethereum library |
| **ethers.js** | 5.7.2 | Ethereum Web3 library |
| **RainbowKit** | 2.1.7 | Wallet connection UI |
| **Web3Modal** | 1.9.12 | Multi-chain wallet connector |
| **React Hot Toast** | 2.5.2 | Toast notifications |
| **React Icons** | 5.5.0 | Icon library |
| **Formspree** | 2.5.4 | Form handling service |

#### Why These Frontend Technologies?

**Next.js 13.4.19**
- Provides server-side rendering (SSR) and static generation
- Better SEO for healthcare application
- Built-in API routes for backend integration
- Automatic code splitting for better performance
- File-based routing system simplifies navigation

**React 18.2.0**
- Component-based architecture for maintainability
- Concurrent rendering for smoother UX
- Large ecosystem and community support
- Efficient re-rendering with virtual DOM

**Tailwind CSS**
- Utility-first approach reduces CSS file bloat
- Responsive design made simple with breakpoints
- Dark mode support built-in
- Highly customizable for healthcare branding

**Wagmi & Viem**
- Industry-standard hooks for Web3 interactions
- Automatic wallet detection and connection
- Type-safe contract interactions
- Built-in transaction management
- Reduced boilerplate compared to Web3.js

**React Query**
- Manages server state and caching efficiently
- Reduces unnecessary re-renders
- Built-in retries and error handling
- Background data synchronization

---

### Blockchain Technology Stack

| Technology | Version | Purpose |
|-----------|---------|---------|
| **Solidity** | ^0.8.0 | Smart contract programming language |
| **Hardhat** | 2.13.0 | Ethereum development framework |
| **Ethers.js** | 5.7.2 | Contract interaction library |
| **Sepolia Testnet** | - | Test network for deployment |

#### Why Solidity & Hardhat?

**Solidity 0.8.0+**
- Industry standard for Ethereum contracts
- Built-in overflow/underflow protection
- Supports advanced features like modifiers and interfaces
- Security-aligned version for production use

**Hardhat**
- Local blockchain for testing without gas costs
- Detailed error messages and debugging capabilities
- Plugin ecosystem for enhanced functionality
- Network management (localhost, testnet, mainnet)
- Automated deployment scripts

---

### Storage & Infrastructure

| Service | Purpose | Integration |
|---------|---------|-------------|
| **IPFS (via Pinata)** | Decentralized file storage | Medical documents, doctor profiles, prescriptions |
| **Pinata API** | IPFS gateway and pinning | Store and retrieve healthcare files |
| **Google Cloud Web3** | Testnet faucet | Sepolia ETH for testing |
| **Reown/WalletConnect** | Multi-chain wallet support | Wallet connection relay |

#### Why IPFS + Pinata?

- **Decentralization**: Files not stored on centralized servers
- **Immutability**: Content-addressed by hash (IPFS provides SHA-256 verification)
- **Redundancy**: Multiple nodes store copies of data
- **Cost-Effective**: No monthly server hosting fees
- **Privacy**: Private files with access control
- **Pinata Integration**: Provides UI, reliability, and API simplicity

---

## System Architecture

### High-Level Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                      USER INTERFACE                             │
│                    (Next.js React App)                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                   │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │         Wagmi & Web3Modal (Wallet Connection)           │  │
│  │  - MetaMask Integration                                 │  │
│  │  - Multi-chain support via RainbowKit                  │  │
│  └──────────────────────────────────────────────────────────┘  │
│                           ↓                                      │
├─────────────────────────────────────────────────────────────────┤
│              CONTRACT INTERACTION LAYER                         │
│             (useContract Hook via Wagmi)                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                   │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │         Ethereum Network (Sepolia Testnet)              │  │
│  │              Smart Contract State                       │  │
│  └──────────────────────────────────────────────────────────┘  │
│                           ↓                                      │
├─────────────────────────────────────────────────────────────────┤
│              DECENTRALIZED STORAGE LAYER                        │
│                                                                   │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │  IPFS Network (via Pinata)                              │  │
│  │  - Medical Documents                                    │  │
│  │  - Doctor Profiles                                      │  │
│  │  - Patient Records                                      │  │
│  └──────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
```

### Data Flow

```
User Action (e.g., Register Doctor)
         ↓
React Component Triggers Action
         ↓
useContract Hook Calls writeContract()
         ↓
Wagmi Prepares Transaction + Signs with Wallet
         ↓
Transaction Sent to Ethereum Network
         ↓
Smart Contract Executes (state changes)
         ↓
Events Emitted
         ↓
Frontend Listens via useWaitForTransactionReceipt
         ↓
UI Updates with Success/Error
```

### Component Architecture

```
Layout (Header + Sidebar)
  ├── Patient Routes
  │   ├── Dashboard (view stats, quick actions)
  │   ├── Register (one-time registration)
  │   ├── Appointments (book, view history)
  │   ├── Medical Records (view history)
  │   ├── Prescriptions (view prescribed medicines)
  │   ├── Medicines (view medicine list)
  │   ├── Orders (purchase history)
  │   └── Profile (view/edit profile)
  │
  ├── Doctor Routes
  │   ├── Dashboard (appointments, patients, stats)
  │   ├── Register (one-time registration)
  │   ├── Appointments (manage appointments)
  │   ├── Patients (view patient list)
  │   ├── Prescribe (prescribe medicines)
  │   ├── Medical Records (update patient history)
  │   └── Profile (view/edit profile)
  │
  └── Admin Routes
      ├── Dashboard (analytics, overview)
      ├── Doctors (manage doctor registrations)
      ├── Appointments (view all appointments)
      ├── Medicines (add/update/manage medicines)
      └── Analytics (system analytics)
```

---

## Smart Contract Design

### Contract: Healthcare.sol (758 lines)

**Location**: `web3/contracts/Healthcare.sol`

**Key Features**:
- Comprehensive healthcare data management
- Role-based access control
- Notification system
- Chat functionality
- Event emissions for all state changes

### Core Data Structures

```solidity
// Medicine Management
struct Medicine {
    uint id;                    // Unique identifier
    string IPFS_URL;           // Link to medicine details on IPFS
    uint price;                // Price in Wei
    uint quantity;             // Available quantity
    uint discount;             // Discount percentage
    string currentLocation;    // Warehouse location
    bool active;               // Active status
}

// Doctor Management
struct Doctor {
    uint id;                        // Unique identifier
    string IPFS_URL;               // Doctor profile on IPFS
    address accountAddress;        // Ethereum address
    uint appointmentCount;         // Total appointments
    uint successfulTreatmentCount; // Successful treatments
    bool isApproved;               // Admin approval status
}

// Patient Management
struct Patient {
    uint id;                   // Unique identifier
    string IPFS_URL;          // Patient profile on IPFS
    string[] medicalHistory;  // Array of medical records
    address accountAddress;   // Ethereum address
    uint[] boughtMedicines;   // Medicine purchase history
}

// Prescription Management
struct Prescription {
    uint id;           // Unique identifier
    uint medicineId;   // Reference to medicine
    uint patientId;    // Reference to patient
    uint doctorId;     // Reference to doctor
    uint date;         // Prescription date
}

// Appointment Management
struct Appointment {
    uint id;                // Unique identifier
    uint patientId;         // Patient involved
    uint doctorId;          // Doctor involved
    uint date;              // Appointment timestamp
    string from;            // Start time
    string to;              // End time
    string appointmentDate; // Date string
    string condition;       // Medical condition
    string message;         // Additional message
    bool isOpen;            // Active/completed status
}

// Chat Support
struct User {
    string name;           // Username
    string userType;       // Patient/Doctor/Admin
    friend[] friendList;  // Contacts
}

struct message {
    address sender;        // Message sender
    uint256 timestamp;     // Timestamp
    string msg;            // Message content
}

// Order Management
struct Order {
    uint medicineId;   // Medicine purchased
    uint price;        // Unit price
    uint payAmount;    // Total paid
    uint quantity;     // Quantity ordered
    uint patientId;    // Patient who ordered
    uint date;         // Order date
}

// Notification System
struct Notification {
    uint id;              // Unique ID
    address userAddress;  // Recipient
    string message;       // Notification text
    uint timestamp;       // When sent
    string categoryType;  // Doctor/Patient/Medicine/etc
}
```

### Key State Variables

```solidity
// Mappings for core data
mapping(uint => Medicine) public medicines;
mapping(uint => Doctor) public doctors;
mapping(uint => Patient) public patients;
mapping(uint => Prescription) public prescriptions;
mapping(uint => Appointment) public appointments;
mapping(address => bool) public registeredDoctors;
mapping(address => bool) public registeredPatients;
mapping(address => Notification[]) private notifications;

// Counters for IDs
uint public medicineCount;
uint public doctorCount;
uint public patientCount;
uint public prescriptionCount;
uint public appointmentCount;

// Admin config
address payable public admin;
uint public registrationDoctorFee = 0.0025 ether;        // ~$6-8 at $2400/ETH
uint public registrationPatientFee = 0.00025 ether;     // ~$0.60-0.80
uint public appointmentFee = 0.0025 ether;              // Same as doctor fee
```

### Core Functions & Workflows

#### Medicine Management Functions

```solidity
// ADD_MEDICINE(string _IPFS_URL, uint _price, uint _quantity, 
//              uint _discount, string _location)
- Only admin can add medicines
- Stores IPFS URL to medicine document
- Emits MEDICINE_ADDED event
- Admin receives notification

// UPDATE_MEDICINE_PRICE(uint _medicineId, uint _price)
- Admin updates price for inventory management
- Triggers MEDICINE_PRICE event

// UPDATE_MEDICINE_ACTIVE(uint _medicineId)
- Toggle medicine availability
- Affects patient purchasing options

// BUY_MEDICINE(uint _medicineId, uint _quantity)
- Patient purchases medicine
- Payment sent to admin
- Medicine added to patient's bought list
- Creates Order struct
- Emits MEDICINE_BOUGHT event
```

#### Doctor Management Functions

```solidity
// ADD_DOCTOR(string _IPFS_URL, address _address, 
//            string _name, string _type)
- Doctor registration with 0.0025 ETH fee (payment to admin)
- IPFS URL contains doctor's credentials/profile
- Doctor status: NOT_APPROVED initially
- Notifications sent to doctor and admin

// APPROVE_DOCTOR_STATUS(uint _doctorId)
- Only admin can approve
- After approval, doctor can accept appointments
- Notifications sent to doctor

// UPDATE_PATIENT_MEDICAL_HISTORY(uint _patientId, 
//                                 string _newMedicalHistory)
- Only approved doctors can execute
- Appends entry to patient's medical history
- Notifications sent to both parties

// COMPLETE_APPOINTMENT(uint _appointmentId)
- Only assigned doctor can complete
- Increments doctor's successfulTreatmentCount
- Marks appointment as closed (isOpen = false)
```

#### Patient Management Functions

```solidity
// ADD_PATIENT(string _IPFS_URL, address _address, 
//             string _name, string _type)
- Patient registration with 0.00025 ETH fee
- Creates new Patient struct
- IPFS URL contains patient's profile/ID
- Notifications sent to patient and admin

// BOOK_APPOINTMENT(uint _doctorId, uint _date, 
//                  string _from, string _to, 
//                  string _appointmentDate, string _condition, 
//                  string _message)
- Patient pays 0.0025 ETH appointment fee
- Creates Appointment struct
- Only approved doctors can be booked
- Notifications sent to doctor and patient

// Prescription Functions
- GET_ALL_PRESCRIBED_MEDICINES_OF_PATIENT(uint patientId)
- Returns all prescriptions for a patient
- READ by patient to see doctor recommendations
```

#### Appointment Management

```solidity
// BOOK_APPOINTMENT - Already covered in Patient section

// GET_PATIENT_APPOINTMENT_HISTORYS(uint _patientId)
- Returns all appointments (completed and active)
- Only patient or admin can view

// GET_PATIENT_APPOINTMENT(uint _appointmentId)
- View single appointment details
- Privacy: only involved patient or admin
```

#### Prescription Management

```solidity
// PRESCRIBE_MEDICINE(uint _medicineId, uint _patientId)
- Only approved doctors
- Creates Prescription record
- Links medicine to patient via doctor prescription
- Emits MEDICINE_PRESCRIBED event

// GET_ALL_PRESCRIBED_MEDICINES_OF_PATIENT(uint patientId)
- Patient views prescribed medicines
- Returns Prescription[] array
```

#### Notification System

```solidity
// ADD_NOTIFICATION(address _userAddress, string _message, 
//                  string _categoryType)
- Internal function called by contract
- Tracks user actions (doctor approvals, appointments, etc.)
- Not accessible to users directly
- Available for frontend integration

// GET_USER_NOTIFICATIONS() - Would need to be implemented
- Retrieve all notifications for connected user
```

#### Chat System

```solidity
// CHECK_USER_EXISTS(address pubkey)
- Verifies user account exists

// CREATE_ACCOUNT(string calldata name, address _address, 
//                 string memory _type)
- Called internally during registration
- Creates User struct for messaging

// ADD_FRIEND(address friend_key, string calldata name, address _myAddress)
- Creates bidirectional friendship
- Allows messaging between users

// _SEND_MESSAGE(address friend_key, address _myAddress, string calldata _msg)
- Sends message between friends
- Stores in allMessages mapping with keccak256 chat code
- Creates notifications

// GET_READ_MESSAGE(address friend_key, address _myAddress)
- Retrieves message history
- Chat code generated from both addresses (order-independent)
```

#### Admin Functions

```solidity
// UPDATE_REGISTRATION_FEE(uint _newFee)
- Change doctor registration fee

// UPDATE_APPOINTMENT_FEE(uint _newFee)
- Change appointment booking fee

// UPDATE_REGISTRATION_PATIENT_FEE(uint _newFee)
- Change patient registration fee

// UPDATE_ADMIN_ADDRESS(address payable _newAddress)
- Migrate admin role to new address
- All future fees go to new admin
```

### Access Control Modifiers

```solidity
modifier onlyAdmin()
- Restricts functions to contract deployer
- Used for: medicine management, doctor approval, fee updates

modifier onlyDoctor()
- Restricts to approved doctors only
- Used for: prescriptions, medical history updates, appointment completion

modifier onlyPatient()
- Restricts to registered patients
- Used for: medicine purchases, appointment booking

// Note: Some functions use if conditions for access rather than modifiers
// Check user status before execution
```

### Events Emitted

The contract emits 20+ events for indexing and frontend listening:

```solidity
// Medicine Events
event MEDICINE_ADDED(uint id, string url, string location);
event MEDICINE_LOCATION(uint id, string newLocation);
event MEDICINE_PRICE(uint id, uint price);
event MEDICINE_DISCOUNT(uint id, uint discount);
event MEDICINE_QUANTITY(uint id, uint quantity);
event MEDICINE_ACTIVE(uint id, bool active);
event MEDICINE_BOUGHT(uint patientId, uint medicineId);

// Doctor Events
event DOCTOR_REGISTERED(uint id, string IPFS_URL, address accountAddress);
event APPROVE_DOCTOR_STATUSD(uint id, bool isApproved);

// Patient Events
event PATIENT_ADDED(uint id, string _IPFS_URL, string[] medicalHistory);
event NOTIFICATiON_SENT(address indexed user, string message, uint timestamp);

// Prescription & Appointment Events
event MEDICINE_PRESCRIBED(uint id, uint medicineId, uint patientId, 
                          uint doctorId, uint date);
event APPOINTMENT_BOOKED(uint id, uint patientId, uint doctorId, uint date);
```

---

## Database & Data Management

### Data Storage Strategy

#### Blockchain Storage (Smart Contract State)

**What's Stored**: 
- All structured data (users, appointments, prescriptions)
- Financial transactions (registration fees, appointment fees)
- Access control and permissions
- Event logs

**Why Blockchain**:
- Immutability prevents tampering
- Transparency allows auditing
- No single point of failure
- Decentralized consensus

**Costs**: 
- Each write operation costs gas
- Estimated 20,000-100,000 gas per major operation
- At 20 Gwei gas price: ~$0.5-5 per operation

#### IPFS Storage (Distributed)

**What's Stored**:
- Patient profiles (JSON with personal info, contact details)
- Doctor profiles (credentials, certifications, biography)
- Medical documents (prescriptions, diagnoses, test results)
- File uploads (X-rays, lab reports, health records)

**Why IPFS**:
- Content-addressed by SHA-256 hash (verification built-in)
- Decentralized - no single server to hack
- Only metadata (IPFS hash) stored on blockchain
- Cost-free using Pinata gateway
- Immutable - once uploaded, content cannot change

**File Structure**:
```
Patient Profile:
{
  "patientId": 1,
  "name": "John Doe",
  "email": "john@example.com",
  "age": 45,
  "bloodType": "O+",
  "allergies": ["Penicillin", "Peanuts"],
  "emergencyContact": {...},
  "additionalDocuments": [...]
}

Doctor Profile:
{
  "doctorId": 1,
  "name": "Dr. Smith",
  "specialization": "Cardiology",
  "licenseNumber": "MD12345",
  "credentials": "MD from Harvard",
  "yearsOfExperience": 15,
  "contactInfo": {...}
}

Medical Record:
{
  "recordId": "abc123...",
  "patientId": 1,
  "doctorId": 1,
  "date": 1683859200,
  "diagnosis": "High Blood Pressure",
  "treatment": "Beta-blockers prescribed",
  "notes": "Follow up in 2 weeks"
}
```

#### Pinata Integration

**Configuration**:
```javascript
// Environment variables needed:
NEXT_PUBLIC_PINATA_JWT = "your_pinata_jwt_token"
NEXT_PUBLIC_PINATA_GATEWAY = "https://gateway.pinata.cloud"

// Using Pinata API
const response = await fetch(
  "https://api.pinata.cloud/pinning/pinFileToIPFS",
  {
    method: "POST",
    headers: {
      Authorization: `Bearer ${PINATA_JWT}`
    },
    body: formData  // File + metadata
  }
);

// Returns:
{
  "IpfsHash": "QmXxxx...",
  "PinSize": 12345,
  "Timestamp": "2024-01-01T00:00:00.000Z"
}

// Store QmXxxx... on blockchain
// Access via: https://gateway.pinata.cloud/ipfs/QmXxxx...
```

### Query Patterns

#### Frontend Read Operations

```javascript
// Get all doctors (read from mapping)
const doctors = await contract.GET_ALL_REGISTERED_DOCTORS();
// Returns: { id, IPFS_URL, accountAddress, appointmentCount, 
//           successfulTreatmentCount, isApproved }

// Get doctor appointments
const appointments = await contract.GET_DOCTOR_APPOINTMENTS_HISTORYS(doctorId);

// Get patient medical history
const history = await contract.GET_PATIENT_MEDICIAL_HISTORY(patientId);
// Returns string[] array from blockchain

// Get IPFS data
const response = await fetch(ipfsUrl);  // ipfsUrl = blockchain data
const jsonData = await response.json(); // Full patient/doctor details
```

### Data Consistency & Validation

1. **On-Chain Validation** (using Solidity require statements):
   - Doctor approval status checked before operations
   - Patient ID existence verified
   - Fee values validated

2. **Off-Chain Validation** (React frontend):
   - Form validation before submission
   - IPFS upload success confirmed
   - Transaction receipt verified

3. **Notification-Based Sync**:
   - Events emitted on contract changes
   - Frontend listens via ethers.js or Wagmi
   - UI updates without polling

---

## Frontend Implementation

### Folder Structure Explained

```
components/
├── admin/                          # Admin-only components
│   ├── AdminAddMedicine.jsx       # Add medicine form
│   ├── AdminAnalytics.jsx         # System analytics
│   ├── AdminAppointmentsManagement.jsx  # Manage all appointments
│   ├── AdminDashboard.jsx         # Admin overview
│   └── AdminDoctorsManagement.jsx # Doctor approval/management
│
├── doctor/                         # Doctor features
│   ├── DoctorAppointments.jsx     # View appointments
│   ├── DoctorDashboard.jsx        # Doctor overview
│   ├── DoctorMedicalRecords.jsx   # Update patient records
│   ├── DoctorPatients.jsx         # View patients
│   ├── DoctorPrescribeMedicine.jsx # Prescribe medicines
│   ├── DoctorProfile.jsx          # View/edit profile
│   ├── DoctorRegistration.jsx     # Onboarding
│   └── DoctorsList.jsx            # Search doctors
│
├── patient/                        # Patient features
│   ├── PatientBookAppointment.jsx # Schedule with doctor
│   ├── PatientDashboard.jsx       # Patient overview
│   ├── PatientHistory.jsx         # Medical history
│   ├── PatientMedicines.jsx       # Browse medicines
│   ├── PatientOrders.jsx          # Purchase history
│   ├── PatientPrescriptions.jsx   # View prescriptions
│   ├── PatientProfile.jsx         # View/edit profile
│   └── PatientRegistration.jsx    # Onboarding
│
├── layout/                         # Layout components
│   ├── Header.jsx                 # Navigation + wallet button
│   ├── Sidebar.jsx                # Navigation menu
│   ├── Layout.jsx                 # Wraps all pages
│   └── CustomConnectButton.jsx    # Styled wallet connector
│
├── common/                         # Reusable UI components
│   ├── Badge.jsx                  # Status badges
│   ├── Button.jsx                 # Custom buttons
│   ├── Card.jsx                   # Card container
│   ├── FileUpload.jsx             # File upload for IPFS
│   ├── Input.jsx                  # Form inputs
│   ├── LoadingSpinner.jsx         # Loading indicator
│   ├── Modal.jsx                  # Dialogs
│   ├── Select.jsx                 # Dropdown component
│   └── index.js                   # Barrel export
│
└── chat/                           # Messaging
    └── HealthcareChat.jsx         # Patient-doctor messaging

pages/
├── index.js                        # Home page
├── doctors.js                      # Doctor directory
├── medicines.js                    # Medicine marketplace
├── chat.js                         # Chat page
├── _app.js                         # App wrapper & providers
│
├── admin/
│   ├── dashboard.js               # Admin dashboard
│   ├── doctors.js                 # Doctor management
│   ├── appointments.js            # Appointment management
│   ├── analytics.js               # Analytics page
│   └── medicines/
│       └── add.js                 # Add medicine page
│
├── doctor/
│   ├── register.js                # Doctor registration
│   ├── dashboard.js               # Doctor dashboard
│   ├── appointments.js            # Manage appointments
│   ├── patients.js                # Patient list
│   ├── prescribe.js               # Prescription page
│   ├── records.js                 # Medical records
│   └── profile.js                 # Doctor profile
│
└── patient/
    ├── register.js                # Patient registration
    ├── dashboard.js               # Patient dashboard
    ├── appointment.js             # Book appointment
    ├── medicines.js               # Browse medicines
    ├── orders.js                  # Purchase history
    ├── prescriptions.js           # View prescriptions
    ├── history.js                 # Medical history
    └── profile.js                 # Patient profile

config/
├── contract.js                     # CONTRACT_ADDRESS & ABI
├── wagmi.js                        # Wagmi configuration
└── ...environment variables

hooks/
└── useContract.js                  # Custom hook for contract interaction
    (Contains 50+ functions for all contract methods)

utils/
├── helpers.js                      # Utility functions
│   - safeNumberConversion()       # BigInt → Number
│   - formatDate/Time/DateTime()   # Date formatting
│   - formatEthAmount()            # Wei → ETH conversion
│   - processContractArray()       # Contract response processing
│   - getRelativeTime()            # "2 hours ago" format
│
└── ipfs.js                         # IPFS/Pinata integration
    - uploadToIPFS()               # Upload files
    - uploadJSONToIPFS()           # Upload JSON data
    - retrieveFromIPFS()           # Download from IPFS

styles/
└── globals.css                     # Global styles

public/
├── data/                           # Mock data (JSON)
│   ├── Doctors.json
│   ├── Medicines.json
│   └── Patients.json
└── images/                         # Static assets
```

### Key Frontend Components

#### 1. Layout & Navigation

**Header.jsx**: 
- Logo and branding
- RainbowKit connect button
- Navigation menu

**Sidebar.jsx**:
- Role-based menu (Patient/Doctor/Admin)
- Navigation links
- User profile section

**Layout.jsx**:
```javascript
// Wraps all pages with:
// - Header component
// - Sidebar component
// - Content area
// - Toaster for notifications
```

#### 2. Authentication & Role-Based Access

**_app.js Setup**:
```javascript
import { WagmiConfig, useAccount } from 'wagmi';
import { RainbowKitProvider } from '@rainbow-me/rainbowkit';
import { QueryClientProvider } from '@tanstack/react-query';

// Wraps all routes with:
// 1. Wagmi for Web3
// 2. RainbowKit for wallet UI
// 3. React Query for state management
```

**Role Detection**:
```javascript
// In each dashboard/page:
const { address, isConnected } = useAccount();
const userType = await getUserType(address);  // Queries contract

// Renders:
if (userType === 'PATIENT') <PatientDashboard />
if (userType === 'DOCTOR') <DoctorDashboard />
if (userType === 'ADMIN') <AdminDashboard />
if (!userType) <RegisterComponent />
```

#### 3. Contract Interaction Hook

**useContract.js** (1152 lines of hook logic):
```javascript
export const useHealthcareContract = () => {
  const { writeContract } = useWriteContract();
  const { data: hash } = writeContract();
  const { isLoading: isConfirming, isSuccess: isConfirmed } = 
    useWaitForTransactionReceipt({ hash });

  // Medicine Functions
  const addMedicine = async (ipfsUrl, price, quantity, discount, location) => {
    return writeContract({
      address: CONTRACT_ADDRESS,
      abi: CONTRACT_ABI,
      functionName: "ADD_MEDICINE",
      args: [ipfsUrl, parseEther(price.toString()), quantity, discount, location]
    });
  };

  // Doctor Functions
  const registerDoctor = async (ipfsUrl, name) => {
    return writeContract({
      address: CONTRACT_ADDRESS,
      abi: CONTRACT_ABI,
      functionName: "ADD_DOCTOR",
      args: [ipfsUrl, address, name, "DOCTOR"],
      value: parseEther("0.0025")
    });
  };

  // Patient Functions
  const registerPatient = async (ipfsUrl, name) => {
    return writeContract({
      address: CONTRACT_ADDRESS,
      abi: CONTRACT_ABI,
      functionName: "ADD_PATIENT",
      args: [ipfsUrl, address, name, "PATIENT"],
      value: parseEther("0.00025")
    });
  };

  // ... 40+ more functions for all contract methods

  return {
    addMedicine,
    registerDoctor,
    registerPatient,
    // ... all functions
  };
};
```

#### 4. IPFS Integration

**ipfs.js**:
```javascript
class IPFSService {
  async uploadToIPFS(file, metadata = {}) {
    const formData = new FormData();
    formData.append("file", file);
    formData.append("pinataMetadata", JSON.stringify({
      name: metadata.name,
      keyvalues: { type: metadata.type, uploadedAt: new Date().toISOString() }
    }));

    const response = await fetch("https://api.pinata.cloud/pinning/pinFileToIPFS", {
      method: "POST",
      headers: { Authorization: `Bearer ${PINATA_JWT}` },
      body: formData
    });

    const result = await response.json();
    return {
      hash: result.IpfsHash,
      url: `${GATEWAY}/ipfs/${result.IpfsHash}`
    };
  }

  async uploadJSONToIPFS(jsonData, metadata = {}) {
    const blob = new Blob([JSON.stringify(jsonData)], { type: 'application/json' });
    const file = new File([blob], metadata.name || 'data.json');
    return this.uploadToIPFS(file, metadata);
  }
}
```

#### 5. Component Examples

**PatientRegistration.jsx**:
```javascript
// 1. Collect patient info (name, email, bloodType, etc.)
// 2. Upload profile to IPFS (returns hash)
// 3. Call registerPatient() with IPFS hash
// 4. Pay 0.00025 ETH registration fee
// 5. Contract creates Patient struct
// 6. Show success message

const handleRegister = async (formData) => {
  setLoading(true);
  try {
    // Upload to IPFS
    const ipfsResult = await ipfsService.uploadJSONToIPFS(formData);
    
    // Call contract
    await registerPatient(ipfsResult.hash, formData.name);
    
    toast.success("Registration successful!");
    router.push("/patient/dashboard");
  } catch (error) {
    toast.error(error.message);
  } finally {
    setLoading(false);
  }
};
```

#### 6. State Management Pattern

```javascript
// Use Wagmi + React Query:
function DoctorDashboard() {
  const { address } = useAccount();
  const { getDoctorAppointments } = useHealthcareContract();
  
  // Automatically re-fetches on mount and dependency changes
  const { data: appointments, isLoading } = useQuery({
    queryKey: ['doctorAppointments', address],
    queryFn: () => getDoctorAppointments()
  });

  if (isLoading) return <LoadingSpinner />;
  
  return (
    <div>
      {appointments?.map(apt => (
        <Card key={apt.id}>
          {/* Render appointment */}
        </Card>
      ))}
    </div>
  );
}
```

---

## Key Features & Functionality

### 1. Patient Features

#### Registration & Profile
- Register with name, email, phone, blood type, allergies
- Profile stored on IPFS, hash stored on blockchain
- One-time 0.00025 ETH registration fee
- Profile is immutable once set (cannot be edited on-chain, only on IPFS)

#### Medical Records
- View complete medical history added by doctors
- Each entry contains diagnosis, treatment, date, doctor notes
- Immutably stored on blockchain
- Can export as certificate

#### Appointments
- Browse all approved doctors
- Check doctor ratings and success rates
- Book appointments with preferred time slots
- Pay 0.0025 ETH per appointment
- Track appointment status (open/completed)
- View appointment history

#### Medicines & Prescriptions
- View all available medicines with details
- See medicines prescribed by doctors
- Order prescribed medicines with discounts
- Track purchase order history

#### Direct Messaging
- Send messages to connected doctors
- Receive responses
- Message history persisted on blockchain
- Notification system for new messages

### 2. Doctor Features

#### Registration & Approval
- Register with credentials, specialization, license number
- Pay 0.0025 ETH registration fee
- Admin approval required before accepting patients
- Profile stored on IPFS

#### Patient Management
- View all registered patients
- Access patient medical history (with privacy checks)
- Update medical history entries
- Prescribe medicines to patients

#### Appointments
- View all scheduled appointments
- Manage appointment status
- Mark appointments as completed
- Track total appointments and successful treatments

#### Prescriptions
- Prescribe medicines to patients
- Link prescription to patient's medical record
- Discounts for patients with valid prescriptions

#### Doctor Ratings
- System tracks successful treatments
- Higher success rate → better for rankings
- Most popular doctors shown on home page

### 3. Admin Features

#### Medicine Management
- Add new medicines with IPFS URLs
- Update price, quantity, discount
- Toggle medicine active/inactive status
- Track medicine inventory

#### Doctor Management
- View all registered doctors
- Approve/reject doctor registrations
- View doctor statistics
- Manage doctor status

#### Fee Management
- Update doctor registration fee (default 0.0025 ETH)
- Update patient registration fee (default 0.00025 ETH)
- Update appointment booking fee (default 0.0025 ETH)
- Update admin wallet address (for fee collection)

#### Analytics & Monitoring
- Total registered users (patients, doctors)
- Total medicine inventory
- Total appointments and revenue
- System health metrics

### 4. System-Wide Features

#### Notification System
- Events triggered for all major actions
- Patients notified of appointment status changes
- Doctors notified of patient updates
- Admin notified of new registrations
- Stored on-chain for audit trail

#### Chat System
- Bidirectional messaging between friends
- Message history stored on blockchain
- Friend list management
- Notification on new messages

#### Payment System
- Fees collected in ETH
- All payments go to admin address
- Immutable transaction records
- No middlemen

#### Events & Monitoring
- 20+ events emitted on state changes
- Events indexed by blockchain explorers
- Enables real-time frontend updates
- Allows subgraph indexing for advanced queries

---

## Security & Efficiency

### Security Measures

#### 1. Smart Contract Security

**Access Control Modifiers**:
```solidity
modifier onlyAdmin() {
    require(msg.sender == admin, "Only admin can perform this action");
    _;
}

modifier onlyDoctor() {
    require(registeredDoctors[msg.sender] && doctors[GET_DOCTOR_ID(msg.sender)].isApproved, 
            "Only approved doctors");
    _;
}

modifier onlyPatient() {
    require(registeredPatients[msg.sender], "Only registered patients");
    _;
}
```

**Input Validation**:
```solidity
// Check user exists
require(_patientId <= patientCount, "Patient does not exist");

// Verify fees
require(msg.value == registrationDoctorFee, "Incorrect registration fee");

// Prevent re-registration
require(!registeredDoctors[_address], "Doctor is already registered");
```

**Reentrancy Prevention**:
- Checks-Effects-Interactions pattern
- State changes before external calls
- No callbacks to external contracts

**Overflow Protection**:
- Solidity 0.8.0+ has built-in overflow checking
- Safe arithmetic operations (no manual SafeMath needed)

#### 2. IPFS Security

- **Content Addressing**: SHA-256 hash prevents tampering
- **Encryption**: Sensitive data encrypted before upload
- **Access Control**: Only authorized users can retrieve specific files
- **Pinata**: Reputable provider ensures availability

#### 3. Frontend Security

**Wallet Authentication**:
- Users must connect MetaMask/wallet to use app
- No centralized username/password login
- Private key never sent to server

**Transaction Signing**:
- All contract calls must be signed by user's wallet
- User explicitly approves each transaction
- No automated execution of actions

**Input Sanitization**:
- React prevents XSS attacks
- Form validation before contract calls
- IPFS URLs validated before pinning

#### 4. Network Security

**Testnet vs Mainnet**:
- Currently deployed on Sepolia testnet
- No real value at risk
- Full testing before mainnet deployment
- Gradual rollout possible

**Smart Contract Upgrades**:
- Contract immutable after deployment (no upgradeable contracts used)
- Ensures user data permanence
- Potential: Deploy new contract version if needed

### Efficiency Optimizations

#### 1. Gas Optimization

**Mapping Instead of Arrays**:
```solidity
// Efficient lookup:
mapping(uint => Doctor) public doctors;  // O(1) access

// Instead of:
Doctor[] public doctors;                  // O(n) search
```

**Loop Optimization**:
```solidity
// Cache array length
uint length = prescriptionCount;
for (uint i = 1; i <= length; i++) {
    // Access prescriptions[i]
}
```

**Batch Operations**:
- Multiple writes in single transaction reduce overhead
- Reducing transaction count = less fees

#### 2. Frontend Optimization

**Code Splitting**:
- Next.js automatically splits code per page
- Only downloaded code needed for current page

**Image Optimization**:
- Next.js Image component with lazy loading
- Automatic format selection (WebP, etc.)

**Caching**:
- React Query caches contract reads
- Prevents redundant blockchain calls
- Background revalidation keeps data fresh

**React Optimization**:
- Memoization with useMemo/useCallback
- Prevents unnecessary re-renders
- Component splitting for better performance

#### 3. Contract Reading Optimization

**View Functions (Free)**:
```solidity
// No gas cost:
function GET_ALL_REGISTERED_DOCTORS() public view returns (Doctor[] memory)
function GET_DOCTOR_DETAILS(uint _doctorId) public view returns (Doctor memory)
```

**Batch Reads**:
- Fetch all doctors once instead of individually
- Filter on frontend instead of making multiple calls

**Event Listening**:
- Subscribe to events for real-time updates
- Don't need to poll contract repeatedly

---

## Installation & Setup

### Prerequisites

Before starting, ensure you have:

1. **Node.js** (v20 or later)
   - Download: https://nodejs.org/
   - Verify: `node --version`

2. **npm** (comes with Node.js)
   - Verify: `npm --version`

3. **Git**
   - Download: https://git-scm.com/

4. **MetaMask Wallet** (or compatible Web3 wallet)
   - Chrome Extension: https://metamask.io
   - Configure for Sepolia Testnet

5. **Ethereum Testnet ETH** (Sepolia)
   - Faucet: https://cloud.google.com/application/web3/faucet/ethereum/sepolia
   - Get free testnet ETH for transactions

6. **Pinata Account** (for IPFS)
   - Sign up: https://pinata.cloud/
   - Create API Key and JWT token

### Step 1: Clone the Repository

```bash
# Navigate to desired directory
cd ~/Desktop

# Clone the project
git clone <repository-url>
cd "Blockchain-Health-DApp/Blockchain Health DApp"
```

### Step 2: Install Frontend Dependencies

```bash
# Install all frontend packages
npm install

# Output should show:
# added X packages, and audited Y packages in Zs
```

### Step 3: Frontend Environment Variables

Create `.env.local` file in the root directory:

```bash
# .env.local

# Contract Configuration
NEXT_PUBLIC_CONTRACT_ADDRESS=0x...  # Will be set after deployment
NEXT_PUBLIC_OWNER_ADDRESS=0x...     # Your wallet address

# Pinata (IPFS)
PINATA_JWT=pnxxxxxx...              # From Pinata API
NEXT_PUBLIC_PINATA_GATEWAY=https://gateway.pinata.cloud

# WalletConnect (optional, for multi-chain support)
NEXT_PUBLIC_WALLET_CONNECT_PROJECT_ID=your_project_id
```

**How to get Pinata JWT**:
1. Go to https://pinata.cloud
2. Login/Sign up
3. Generate new API key
4. Copy JWT token
5. Paste in `.env.local`

### Step 4: Install Smart Contract Dependencies

```bash
# Navigate to web3 directory
cd web3

# Install Hardhat and dependencies
npm install

# Output shows:
# added X packages, and audited Y packages in Zs
```

### Step 5: Smart Contract Environment Variables

Create `.env` file in `web3/` directory:

```bash
# web3/.env

# Network Configuration
NETWORK_RPC_URL=https://eth-sepolia.g.alchemy.com/v2/YOUR_ALCHEMY_KEY
# OR
NETWORK_RPC_URL=https://sepolia.drpc.org

# Private Key (from MetaMask - NEVER share this!)
PRIVATE_KEY=0x...  # Your wallet private key

# Optional: For Etherscan verification
ETHERSCAN_API_KEY=xxxxx
```

**How to get Private Key**:
1. Open MetaMask
2. Click three dots → Account details
3. Click Export Private Key
4. Enter password, copy key
5. Paste in `web3/.env` (KEEP SECRET!)

**How to get Alchemy RPC**:
1. Go to https://www.alchemy.com/
2. Create account and project
3. Select Sepolia network
4. Copy HTTP URL
5. Paste in `.env`

### Step 6: Verify Installation

```bash
# Test frontend can start
npm run dev
# Should see: ready - started server on 0.0.0.0:3000

# In another terminal, test smart contract compilation
cd web3
npx hardhat compile
# Should see: compiled successfully
```

---

## Deployment Guide

### Phase 1: Local Testing (Hardhat Network)

#### Step 1: Start Hardhat Local Blockchain

```bash
# In one terminal window, from web3/ directory
cd web3
npx hardhat node

# Output:
# Started HTTP and WebSocket JSON-RPC server at http://127.0.0.1:8545/
# 
# Accounts (10 test accounts with 10000 ETH each):
# Account #0: 0x1234... (deployer account)
# Account #1: 0x5678... (for testing)
# ...
```

**These are test accounts. Keep this terminal running.**

#### Step 2: Deploy to Local Blockchain

```bash
# In a new terminal, from web3/ directory
npx hardhat run scripts/deploy.js --network localhost

# Output:
# Deploying contracts with the account: 0x1234...abc (deployer)
# Account balance: 10000000000000000000
# 
# Deploying Healthcare contract...
# 
# Deployment Successful!
# ------------------------
# NEXT_PUBLIC_Healthcare_ADDRESS: 0xabc123...
# NEXT_PUBLIC_OWNER_ADDRESS: 0x1234...abc
```

**Save these addresses!** You need them for `.env.local`

#### Step 3: Configure MetaMask for Local Network

1. Open MetaMask
2. Click Settings → Networks
3. Add Network:
   - Network Name: Hardhat Local
   - RPC URL: http://127.0.0.1:8545
   - Chain ID: 1337
   - Currency: ETH

4. Switch to Hardhat Local network
5. Import test account:
   - Click account icon → Import Account
   - Paste private key from hardhat node output
   - Import successfully

Now MetaMask shows 10000 ETH balance (test only)

#### Step 4: Update Frontend Configuration

Update `.env.local`:

```bash
# .env.local (for local testing)
NEXT_PUBLIC_CONTRACT_ADDRESS=0xabc123...      # From deployment
NEXT_PUBLIC_OWNER_ADDRESS=0x1234...abc        # From deployment
PINATA_JWT=pnxxxxx...
NEXT_PUBLIC_PINATA_GATEWAY=https://gateway.pinata.cloud
```

#### Step 5: Run Frontend on Local Network

```bash
# Make sure you're in root directory (not web3/)
# Exit any previous npm dev, then:

npm run dev

# Output:
# ready - started server on 0.0.0.0:3000
```

Open http://localhost:3000 in browser

#### Step 6: Test Registration & Basic Flows

1. **Connect Wallet**:
   - Click "Connect Wallet" button
   - MetaMask popup appears
   - Select Hardhat Local account
   - Click Connect

2. **Register as Doctor**:
   - Go to Doctor Registration page
   - Fill form: Name, Specialization, License, etc.
   - Click Upload and Submit
   - Confirm transaction in MetaMask
   - Should see success message

3. **Register as Patient**:
   - Disconnect current wallet (or use different account)
   - Connect different test account
   - Go to Patient Registration
   - Fill form
   - Confirm transaction

4. **Approve Doctor (as Admin)**:
   - Switch to admin account (deployer account from deployment)
   - Go to Admin Dashboard
   - Find pending doctor
   - Click Approve
   - Confirm transaction

5. **Book Appointment**:
   - Switch to patient account
   - Click "Book Appointment"
   - Select approved doctor
   - Choose date/time
   - Confirm payment

6. **Prescribe Medicine**:
   - Switch to doctor account
   - Click "Prescribe Medicine"
   - Select patient and medicine
   - Confirm transaction

### Phase 2: Testnet Deployment (Sepolia)

#### Step 1: Get Testnet ETH

```
1. Go to https://cloud.google.com/application/web3/faucet/ethereum/sepolia
2. Connect wallet (MetaMask on Sepolia)
3. Claim 0.5 ETH (free)
4. Wait 1-2 minutes for transaction
5. Check MetaMask - balance should update
```

#### Step 2: Configure Sepolia in MetaMask

MetaMask automatically detects Sepolia, but verify:
1. MetaMask → Networks
2. Should see "Sepolia" in list
3. Switch to Sepolia
4. Verify balance > 0.1 ETH

#### Step 3: Deploy Smart Contract to Sepolia

```bash
# From web3/ directory
npx hardhat run scripts/deploy.js --network sepolia

# Output:
# Deploying contracts with the account: 0x1234...
# Account balance: 500000000000000000 (0.5 ETH)
# 
# Deploying Healthcare contract...
# 
# Deployment Successful!
# ------------------------
# NEXT_PUBLIC_Healthcare_ADDRESS: 0xcba321...
# NEXT_PUBLIC_OWNER_ADDRESS: 0x1234...
```

**Wait 30 seconds for Sepolia confirmation**

#### Step 4: Verify Contract on Block Explorer

```bash
# Find transaction on Sepolia Etherscan
# URL: https://sepolia.etherscan.io
# Search for contract address or tx hash

# Shows:
# - Contract deployed at: 0xcba321...
# - Transaction confirmed
# - Contract source (if verified)
```

#### Step 5: Update Frontend for Sepolia

```bash
# .env.local (for Sepolia testnet)
NEXT_PUBLIC_CONTRACT_ADDRESS=0xcba321...     # Sepolia contract address
NEXT_PUBLIC_OWNER_ADDRESS=0x1234...          # Your wallet on Sepolia
PINATA_JWT=pnxxxxx...
NEXT_PUBLIC_PINATA_GATEWAY=https://gateway.pinata.cloud
NEXT_PUBLIC_WALLET_CONNECT_PROJECT_ID=xxxxx  # Optional
```

Update `config/wagmi.js`:

```javascript
// config/wagmi.js
import { sepolia } from 'wagmi/chains'

export const config = getDefaultConfig({
  appName: 'Health DApp',
  projectId: PROJECT_ID,
  chains: [sepolia],  // Changed from localhost
  ssr: true,
})
```

#### Step 6: Switch MetaMask to Sepolia

1. Open MetaMask
2. Click network selector dropdown
3. Select "Sepolia"
4. Confirm ~0.5 ETH balance

#### Step 7: Test on Sepolia

```bash
# From root directory
npm run dev

# Open http://localhost:3000
```

Test the same flows as local:
1. Connect wallet (MetaMask on Sepolia)
2. Register as doctor (costs ~0.0025 ETH)
3. Register as patient (costs ~0.00025 ETH)
4. Approve doctor (admin only)
5. Book appointment (costs ~0.0025 ETH)

**Each transaction takes 15-30 seconds on Sepolia**

---

## Running the Application

### Complete Startup Sequence (Development)

#### Terminal 1: Smart Contract Blockchain

```bash
# Keep a local Hardhat node running
cd web3
npx hardhat node

# Runs until you press Ctrl+C
# Output shows test accounts and RPC endpoint
```

#### Terminal 2: Smart Contract Deployment

```bash
# In new terminal, from web3/
npx hardhat run scripts/deploy.js --network localhost

# Shows deployed contract address
# Copy address to .env.local
```

#### Terminal 3: Frontend Development Server

```bash
# In new terminal, from root directory
npm run dev

# Output:
# ready - started server on 0.0.0.0:3000
# 
# Navigate to http://localhost:3000
```

#### Terminal 4: Optional - Testing

```bash
# In new terminal, from web3/
npx hardhat test

# Runs test suite (if you add tests)
```

### Running for Production

#### Build Frontend

```bash
# From root directory
npm run build

# Creates optimized build:
# - Compiles React components
# - Bundles CSS, JS
# - Generates static pages
# - Output: .next/

# Takes 2-3 minutes first time
```

#### Start Production Build

```bash
npm start

# Output:
# > next start
# Ready to accept connections
# started server on 0.0.0.0:3000
#
# Visit http://localhost:3000
```

#### Deploy to Hosting

For production deployment:

1. **Vercel (Recommended)**:
   ```bash
   npm install -g vercel
   vercel
   # Pushes to Vercel, gets automatic SSL/CDN
   ```

2. **Traditional Server**:
   ```bash
   # Build locally
   npm run build
   
   # Copy to server
   scp -r .next/ server:/app/
   scp package.json server:/app/
   
   # On server
   npm install --production
   npm start
   ```

3. **Docker**:
   ```dockerfile
   FROM node:20
   WORKDIR /app
   COPY . .
   RUN npm ci && npm run build
   EXPOSE 3000
   CMD ["npm", "start"]
   ```

### Development Commands Reference

```bash
# Frontend
npm run dev              # Start development server (localhost:3000)
npm run build           # Build for production
npm start               # Run production build
npm run lint            # Check code style
npm run clear           # Clear node_modules, build cache

# Smart Contract (from web3/)
npx hardhat compile     # Compile Solidity contracts
npx hardhat node        # Start local blockchain
npx hardhat test        # Run tests
npx hardhat clean       # Clear artifacts/cache

# Deployment (from web3/)
npx hardhat run scripts/deploy.js --network localhost
npx hardhat run scripts/deploy.js --network sepolia
```

### Troubleshooting

**Issue: "Cannot find module 'wagmi'"**
```bash
# Solution: Reinstall dependencies
npm install
# If still failing:
npm run clear
npm install
```

**Issue: "MetaMask not found"**
```
- Install MetaMask extension: https://metamask.io
- Reload browser page (F5)
- Clear browser cache if needed
```

**Issue: "Contract not found at address"**
```
- Check .env.local has correct NEXT_PUBLIC_CONTRACT_ADDRESS
- Verify contract deployed successfully
- Contract must be deployed to current network
- Switch MetaMask to correct network
```

**Issue: "Insufficient funds for gas"**
```
- You need ETH on the network (Sepolia or Hardhat)
- Get free ETH: https://cloud.google.com/application/web3/faucet/ethereum/sepolia
- Wait a few minutes for transaction to confirm
- Refresh MetaMask (reload page)
```

**Issue: "Transaction reverted"**
```
- Check error message in console
- Common reasons:
  * Wrong fee amount (check contract fee amounts)
  * Doctor not approved (admin must approve first)
  * Patient not registered (need to register first)
  * Duplicate registration (user already exists)
```

---

## API & Contract Functions

### Patient Functions

#### Registration

```javascript
registerPatient(ipfsUrl, name)
  Input:
    - ipfsUrl: String - IPFS hash of patient profile JSON
    - name: String - Patient full name
  Output:
    - Transaction receipt
  Cost: 0.00025 ETH
  Note: One-time only, cannot re-register same address
```

#### Appointments

```javascript
bookAppointment(doctorId, date, from, to, appointmentDate, condition, message)
  Input:
    - doctorId: Number - ID of approved doctor
    - date: Number - Unix timestamp
    - from: String - Start time (e.g., "10:00 AM")
    - to: String - End time (e.g., "10:30 AM")
    - appointmentDate: String - Date string (e.g., "2024-01-15")
    - condition: String - Medical condition
    - message: String - Any additional notes
  Output:
    - Transaction receipt with appointment ID
  Cost: 0.0025 ETH per appointment
  Requires: Registered patient, approved doctor

GET_PATIENT_APPOINTMENT_HISTORYS(patientId)
  Returns: Array of Appointment objects
  Access: Patient or Admin only
```

#### Medicines

```javascript
GET_ALL_REGISTERED_MEDICINES()
  Returns: Array of all medicines in system
  Cost: Free (view function)

BUY_MEDICINE(medicineId, quantity)
  Input:
    - medicineId: Number
    - quantity: Number
  Output:
    - Transaction receipt with Order ID
  Cost: (Medicine price × quantity) - discount if applicable
```

#### Medical History

```javascript
GET_PATIENT_MEDICIAL_HISTORY(patientId)
  Returns: Array of medical history strings
  Access: Patient or Admin only
  Cost: Free (view function)
```

#### Prescriptions

```javascript
GET_ALL_PRESCRIBED_MEDICINES_OF_PATIENT(patientId)
  Returns: Array of Prescription objects
  Cost: Free (view function)
```

### Doctor Functions

#### Registration

```javascript
registerDoctor(ipfsUrl, name)
  Input:
    - ipfsUrl: String - IPFS hash of doctor profile JSON
    - name: String - Doctor name
  Output:
    - Transaction receipt
  Cost: 0.0025 ETH
  Note: Requires admin approval before accepting patients
```

#### Appointments

```javascript
GET_DOCTOR_APPOINTMENTS_HISTORYS(doctorId)
  Returns: Array of appointments assigned to doctor
  Cost: Free (view function)

COMPLETE_APPOINTMENT(appointmentId)
  Input:
    - appointmentId: Number
  Output:
    - Transaction receipt
  Access: Assigned doctor only
  Effect: Marks appointment closed, increments successfulTreatmentCount
```

#### Medical Records

```javascript
UPDATE_PATIENT_MEDICAL_HISTORY(patientId, newMedicalHistory)
  Input:
    - patientId: Number
    - newMedicalHistory: String - New entry to add
  Output:
    - Transaction receipt
  Access: Approved doctors only
  Note: Appends to array, cannot modify/delete existing entries
```

#### Prescriptions

```javascript
PRESCRIBE_MEDICINE(medicineId, patientId)
  Input:
    - medicineId: Number
    - patientId: Number
  Output:
    - Transaction receipt with Prescription ID
  Access: Approved doctors only
  Effect: Creates prescription record, allows patient to buy medicine
```

#### Patients List

```javascript
GET_ALL_REGISTERED_PATIENTS()
  Returns: Array of all patients
  Cost: Free (view function)

GET_DOCTOR_DETAILS(doctorId)
  Returns: Doctor object with stats
  Cost: Free (view function)
  Fields:
    - id: Number
    - IPFS_URL: String
    - accountAddress: Address
    - appointmentCount: Number
    - successfulTreatmentCount: Number
    - isApproved: Boolean
```

### Admin Functions

#### Medicine Management

```javascript
ADD_MEDICINE(ipfsUrl, price, quantity, discount, location)
  Input:
    - ipfsUrl: String - IPFS hash
    - price: BigInt - Price in Wei (use parseEther() in frontend)
    - quantity: Number
    - discount: Number (0-100 percentage)
    - location: String - Warehouse location
  Output:
    - Transaction receipt with Medicine ID
  Access: Admin only

UPDATE_MEDICINE_PRICE(medicineId, price)
  Input:
    - medicineId: Number
    - price: BigInt - New price in Wei
  Access: Admin only

UPDATE_MEDICINE_QUANTITY(medicineId, quantity)
  Updates available quantity
  Access: Admin only

UPDATE_MEDICINE_DISCOUNT(medicineId, discount)
  Updates discount percentage
  Access: Admin only

UPDATE_MEDICINE_ACTIVE(medicineId)
  Toggles active/inactive status
  Access: Admin only
```

#### Doctor Management

```javascript
APPROVE_DOCTOR_STATUS(doctorId)
  Input:
    - doctorId: Number
  Output:
    - Transaction receipt
  Access: Admin only
  Effect: Allows doctor to accept appointments and prescribe

GET_ALL_REGISTERED_DOCTORS()
  Returns: Array of all doctors (approved and pending)
  Cost: Free

GET_ALL_APPROVED_DOCTORS()
  Returns: Array of approved doctors only
  Cost: Free

GET_MOST_POPULAR_DOCTOR()
  Returns: Doctor with highest combined stats
  Cost: Free
  Ranking: appointmentCount + successfulTreatmentCount
```

#### Fee Management

```javascript
UPDATE_REGISTRATION_FEE(newFee)
  Updates doctor registration fee (default 0.0025 ETH)

UPDATE_REGISTRATION_PATIENT_FEE(newFee)
  Updates patient registration fee (default 0.00025 ETH)

UPDATE_APPOINTMENT_FEE(newFee)
  Updates appointment fee (default 0.0025 ETH)

UPDATE_ADMIN_ADDRESS(newAddress)
  Migrates all future fees to new address
```

### Shared Functions (Patients & Doctors)

#### Chat

```javascript
GET_USERNAME_TYPE(address)
  Returns: User object { name, userType }
  Cost: Free

GET_MY_FRIEND_LIST(address)
  Returns: Array of friend objects
  Cost: Free

_SEND_MESSAGE(friendAddress, myAddress, message)
  Input:
    - friendAddress: Address of recipient
    - myAddress: Your address
    - message: String
  Output:
    - Transaction receipt
  Access: Both must be registered and friends

GET_READ_MESSAGE(friendAddress, myAddress)
  Returns: Array of all messages in conversation
  Cost: Free
```

### Public View Functions (No Authentication)

```javascript
GET_ALL_REGISTERED_MEDICINES()
  Returns all medicines

GET_MEDICINE_DETAILS(medicineId)
  Returns single medicine

GET_ALL_REGISTERED_DOCTORS()
  Returns all doctors (including pending)

GET_ALL_APPROVED_DOCTORS()
  Returns doctors approved and ready to accept patients

GET_MOST_POPULAR_DOCTOR()
  Returns top-rated doctor

GET_DOCTOR_DETAILS(doctorId)
  Returns doctor with stats

GET_ALL_APPOINTMENTS()
  Returns all appointments in system

contractCall(functionName, args)
  Generic pattern for all view functions
  Cost: Free
```

---

## Conclusion

### Summary

This Blockchain Healthcare DApp represents a comprehensive solution for decentralized medical data management. By combining Solidity smart contracts, IPFS storage, and a modern Next.js frontend, the system ensures:

1. **Transparency**: All transactions immutably recorded on blockchain
2. **Security**: Patient data encrypted and distributed across IPFS
3. **Efficiency**: Automated smart contracts eliminate intermediaries
4. **Accessibility**: Web3 wallet integration enables global access
5. **Privacy**: Users control access to their medical records

### Key Achievements

- **758-line smart contract** with comprehensive healthcare functionality
- **Role-based access control** for patients, doctors, and admins
- **Integrated IPFS storage** for medical documents
- **Real-time notifications** for all healthcare events
- **Full-featured React frontend** with Wagmi Web3 integration
- **Testnet deployment** on Sepolia ready for testing

### Future Enhancements

1. **Mainnet Deployment**: Deploy to Ethereum/Polygon for production use
2. **Mobile App**: React Native version for iOS/Android
3. **AI Integration**: Machine learning for diagnosis recommendations
4. **Telemedicine**: Video chat integration using WebRTC
5. **Insurance Integration**: Connect with insurance providers
6. **GraphQL Subgraph**: Advanced querying with The Graph protocol
7. **Governance Token**: DAO for decentralized management
8. **Layer 2 Scaling**: Deploy on Arbitrum/Optimism for lower fees

### Technology Recommendations Justified

| Technology | Justification |
|-----------|-------------|
| **Solidity** | Industry standard, battle-tested, largest ecosystem |
| **Hardhat** | Best DX, powerful testing, local blockchain available |
| **Next.js** | Server-side rendering improves healthcare app SEO |
| **Wagmi** | Modern Web3 hooks, reduces boilerplate significantly |
| **IPFS** | Decentralized, immutable, perfect for medical records |
| **Tailwind** | Rapid UI development, consistent healthcare design |
| **React Query** | Efficient state management for contract data |

### Setup Checklist

- [ ] Install Node.js v20+
- [ ] Create `.env.local` with contract address
- [ ] Create `.env` in web3/ with private key
- [ ] Get Pinata JWT token
- [ ] Configure MetaMask for Sepolia
- [ ] Claim testnet ETH from faucet
- [ ] Deploy smart contract to Sepolia
- [ ] Update frontend with contract address
- [ ] Run `npm run dev` and test registration

### Support & Resources

- **Deployment**: https://youtu.be/zSu5oMnFek4?si=yZU0fayXDKr0JzRr
- **Docs**: https://www.theblockchaincoders.com/
- **Sepolia Faucet**: https://cloud.google.com/application/web3/faucet/ethereum/sepolia
- **Wagmi Docs**: https://wagmi.sh/
- **Solidity Docs**: https://docs.soliditylang.org/

---

## Appendix: File Structure Summary

```
project-root/
├── components/           # React components (40+ files)
├── pages/               # Next.js pages and routes (25+ files)
├── config/              # Configuration files
│   ├── contract.js      # Contract ABI and address
│   └── wagmi.js         # Wagmi/Rainbow kit config
├── hooks/               # React hooks
│   └── useContract.js   # Healthcare contract interactions (1152 lines)
├── utils/               # Utility functions
│   ├── helpers.js       # Date, formatting utilities
│   └── ipfs.js          # IPFS/Pinata integration
├── styles/              # CSS styles
│   └── globals.css      # Global styles
├── public/              # Static assets
├── web3/                # Smart contract folder
│   ├── contracts/
│   │   └── Healthcare.sol    # Main contract (758 lines)
│   ├── scripts/
│   │   └── deploy.js        # Deployment script
│   ├── artifacts/           # Compiled contracts
│   └── package.json
├── .env.local           # Frontend environment variables
├── .env (in web3/)      # Hardhat environment variables
├── package.json         # Frontend dependencies
├── next.config.js       # Next.js configuration
├── tailwind.config.js   # Tailwind CSS config
├── jsconfig.json        # JavaScript configuration
└── README.md            # Project documentation
```

---

**Document Generated**: March 2026
**Project Status**: Ready for Sepolia Testnet Deployment
**Latest Framework Versions**: Next.js 13.4.19, React 18.2.0, Solidity 0.8.0+

---
