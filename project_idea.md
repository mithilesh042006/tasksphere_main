# 🧠 TaskSphere – Simple Task Sharing for Mobile

## 🔍 Overview

**TaskSphere** is a mobile-first task sharing app inspired by the simplicity of messaging platforms like WhatsApp. The app enables users to connect with one another and share tasks directly and personally, without complex group structures or admin roles. It focuses on effortless peer-to-peer task communication and organization.

---

## 🧹 Core Concepts

### 👤 User (Single Role)

* Every user has a single account with full functionality.
* Identified by a **unique 8-digit alphanumeric User ID**.
* Can send and receive tasks from other users.
* Manages personal task list.

### ✅ Tasks

* Tasks are created and shared directly between users.
* A task includes: title, description, due date, and optional priority.
* Tasks are updated by the receiver to track their own progress.
* No group or swap functionality required.

---

## 🚀 Key Features

### 🔐 Authentication

* Simple user registration and login.
* Secure login via JWT or session tokens.

### 📢 Messaging-Style Task Sharing

* Users can search for others using their User ID.
* Task sharing works like a direct message.
* Each shared task appears in a chat-like thread.

### 📝 Task Management

* Create tasks and send to one or multiple recipients.
* Each user maintains their own task status (Pending, In Progress, Completed).
* Task reminders and editing available for sender and receiver.

### 📊 Dashboard

* Personal task dashboard with status filters.
* Recent task activity timeline.

### 🗓️ Calendar & Reminders

* Built-in calendar view of assigned and received tasks.
* Automated reminders for deadlines.

### 🔔 Notifications

* Notification when a new task is received.
* Alerts for upcoming deadlines and changes.

---
This simpler structure supports fast task sharing and real-time collaboration between individuals, perfect for small teams, freelancers, or any user who prefers direct, no-fuss coordination.
