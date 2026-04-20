# Health Nexus - Unified Healthcare Management System

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Language: Python](https://img.shields.io/badge/Language-Python-blue.svg)](https://www.python.org/)
[![Framework: Django](https://img.shields.io/badge/Framework-Django-green.svg)](https://www.djangoproject.com/)
[![Database: MySQL](https://img.shields.io/badge/Database-MySQL-orange.svg)](https://www.mysql.com/)

**Health Nexus** is a comprehensive healthcare management platform designed to bridge the gap between patients, doctors, and healthcare organizations (hospitals, clinics, and laboratories). It provides a unified interface for managing medical records, staff, and organizational data with strict role-based access control.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Role-Based Access](#role-based-access)
- [System Architecture](#system-architecture)
- [Prerequisites](#prerequisites)
- [Installation & Setup](#installation--setup)
- [Database Schema](#database-schema)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [How It Works](#how-it-works)
- [Contributing](#contributing)
- [Author](#author)

## Overview

Health Nexus simplifies healthcare administration by providing a digital ecosystem where multiple organizations can coexist. It allows for the seamless management of patient histories, staff assignments, and doctor specializations. The system ensures that sensitive medical data is only accessible to authorized personnel through a robust designation-based logic.

## Features

- **Multi-Organization Support**: Manage Public/Private Hospitals, Clinics, and Laboratories.
- **Role-Based Dashboards**: Customized interfaces for Doctors, Patients, Staff, and Admins.
- **Patient History Tracking**: Centralized storage for patient reports (PDFs) and lab results.
- **Staff Management**: Tracking medical and non-medical staff across organizations.
- **Specialization Mapping**: Categorizing organizations and doctors by medical expertise.
- **Secure Authentication**: Automated password generation based on user details (e.g., phone and DOB).
- **Dynamic CRUD Operations**: Full management of Specializations, Degrees, Doctors, and Patients.

## Role-Based Access

The system defines five distinct user designations:

1.  **Super Admin**: Oversees the entire platform and manages organizations.
2.  **Organization Admin**: Manages staff and doctors within a specific hospital/clinic.
3.  **Doctor**: Accesses assigned patient records and manages medical histories.
4.  **Organization Staff**: Handles day-to-day operations and administrative tasks.
5.  **Patient**: Views personal medical history and uploaded laboratory reports.

## System Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     MySQL Database                          │
│  ┌─────────────┐   ┌──────────────┐   ┌──────────────┐    │
│  │ Organizations │   │   Doctors    │   │  Patients    │    │
│  └─────────────┘   └──────────────┘   └──────────────┘    │
│          ▲                ▲                   ▲           │
└──────────┼────────────────┼───────────────────┼───────────┘
           │                │                   │
           ▼                ▼                   ▼
┌─────────────────────────────────────────────────────────────┐
│                    Django Backend (MVT)                     │
│  ┌────────────┐    ┌────────────┐    ┌────────────┐       │
│  │   Models   │    │   Views    │    │ Templates  │       │
│  │ (ORM/Log)  │    │  (Logic)   │    │   (UI)     │       │
│  └────────────┘    └────────────┘    └────────────┘       │
└─────────────────────────────────────────────────────────────┘
           │                │                   │
           ▼                ▼                   ▼
┌─────────────────────────────────────────────────────────────┐
│                     Client Browser                          │
│        Dynamic Dashboards & PDF Report Maintenance        │
└─────────────────────────────────────────────────────────────┘
```

## Prerequisites

Before you begin, ensure you have the following installed:

- **Python 3.8+**: [Download](https://www.python.org/downloads/)
- **MySQL Server 8.0+**: [Download](https://dev.mysql.com/downloads/installer/)
- **pip** (Python Package Manager)

## Installation & Setup

### Step 1: Clone the Repository

```bash
git clone https://github.com/Harshwardhan-Deshmukh03/HealthNexus.git
cd health_nexus/HealthNexus/healthNexus
```

### Step 2: Install Dependencies

```bash
pip install django mysqlclient
```

### Step 3: Configure Database

1.  **Create the Database**:
    ```sql
    CREATE DATABASE Health_Nexus_Database;
    ```

2.  **Update Settings**: 
    Edit `healthNexus/settings.py` and update your MySQL credentials:
    ```python
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.mysql',
            'NAME': 'Health_Nexus_Database',
            'USER': 'your_username',
            'PASSWORD': 'your_password',
            'HOST': 'localhost',
            'PORT': '3306',
        }
    }
    ```

### Step 4: Run Migrations

```bash
python manage.py makemigrations
python manage.py migrate
```

### Step 5: Start the Development Server

```bash
python manage.py runserver
```

Access the application at `http://127.0.0.1:8000/`

## Database Schema

### Core Tables

-   **`base_organization`**: Stores organization ID, name, type, and specializations.
-   **`base_doctor`**: Stores doctor profile, specialization, and associated organization.
-   **`base_patient`**: Personal information for users seeking medical services.
-   **`base_patient_history`**: Links patients, doctors, and organizations with report PDFs.
-   **`base_organization_staff`**: Personnel data for nurses, technicians, and assistants.
-   **`base_customuserprofile`**: Extends Django's `User` model with `designation`.

## Usage

### Login System
- **Doctors/Patients**: Use the provided ID as the username. 
- **Initial Password**: Typically follows the format `phoneNumber@DDMMYYYY` (generated automatically upon registration).

### Admin Workflow
1.  **Create Specializations**: Define medical fields (e.g., Cardiology).
2.  **Register Organizations**: Link organizations to specializations.
3.  **Add Staff/Doctors**: Assign medical professionals to specific organizations.
4.  **Record History**: Doctors upload PDFs of patient diagnoses and lab results.

## Project Structure

```
HealthNexus/
└── healthNexus/
    ├── base/               # Main application logic
    │   ├── migrations/     # DB migration files
    │   ├── templates/      # HTML UI (organized by role)
    │   ├── forms.py        # Django forms for CRUD
    │   ├── models.py       # Database Schema definitions
    │   ├── views.py        # Business logic & authentication
    │   └── urls.py         # URL routing for 'base' app
    ├── healthNexus/        # Project settings & configuration
    │   ├── settings.py     # Main configuration
    │   └── urls.py         # Root URL configuration
    ├── media/              # Uploaded reports and images
    └── manage.py           # Django management script
```

## Contributing

1.  **Fork the Project**
2.  **Create your Feature Branch** (`git checkout -b feature/AmazingFeature`)
3.  **Commit your Changes** (`git commit -m 'Add some AmazingFeature'`)
4.  **Push to the Branch** (`git push origin feature/AmazingFeature`)
5.  **Open a Pull Request**

## Author

**Harshwardhan Deshmukh**

- GitHub: [@Harshwardhan-Deshmukh03](https://github.com/Harshwardhan-Deshmukh03)

**Aditya Choudhary**

- GitHub: [@aditya-choudhary599](https://github.com/aditya-choudhary599))

**Vipul Chaudhari**

- GitHub: [@VipulChaudhari31](https://github.com/VipulChaudhari31))

---

⭐ **Star this repository if you find it helpful!**
