# CheckList - Updated Documentation

## 📋 USER ROLES & PERMISSIONS

### **1. ADMIN (Full Control)**
- Login: `admin` / `Admin@1234`
- Access to ALL features
- Can manage everything
- **Menu:** Dashboard, Doers, Tasks, Master Schedule, Done List, Scoring

---

### **2. SUPER ADMIN (Limited + WhatsApp)**
- Login: (Any doer with user_type = "Super Admin") / `User@1234`
- Same screen as User + WhatsApp button
- **Menu:** My Tasks, Done List
- **Extra:** ✅ WhatsApp button to send tasks to assignee
- **Cannot:** Edit, Create, Delete anything
- **Can:** Complete tasks and send WhatsApp notifications

---

### **3. USER (Read-Only)**
- Login: (Any doer with user_type = "User") / `User@1234`
- Same screen as Super Admin but WITHOUT WhatsApp button
- **Menu:** My Tasks, Done List
- **Can:** View pending tasks, Complete tasks
- **Cannot:** Edit, Delete, or Send WhatsApp

---

## 🔑 LOGIN CREDENTIALS

```
ADMIN:
  Username: admin
  Password: Admin@1234

USER / SUPER ADMIN:
  Username: [Any doer name from database]
  Password: User@1234
  
  Example:
  Username: Swapan Kr Ghorai
  Password: User@1234
```

---

## 📊 FEATURE MATRIX

| Feature | Admin | Super Admin | User |
|---------|-------|------------|------|
| Dashboard | ✅ | ❌ | ❌ |
| Manage Doers | ✅ | ❌ | ❌ |
| Manage Tasks | ✅ | ❌ | ❌ |
| Master Schedule | ✅ | ❌ | ❌ |
| Scoring | ✅ | ❌ | ❌ |
| **My Tasks** | ❌ | ✅ | ✅ |
| **Done List** | ✅ | ✅ (View) | ✅ (View) |
| **Complete Task** | ❌ | ✅ | ✅ |
| **WhatsApp** | ❌ | ✅ | ❌ |

---

## 🎯 USER & SUPER ADMIN SCREEN

Both see the **exact same interface** with these sections:

### **My Tasks**
- Shows all pending tasks assigned to logged-in user
- Displays: Task name, Department, Frequency, Planned date
- Status badge: "OVERDUE" (red) or "X days left" (orange)
- Buttons:
  - **Complete** button (for User & Super Admin)
  - **WhatsApp** button (ONLY for Super Admin) 🟢

### **Done List**
- Shows completed tasks (READ-ONLY for both)
- Cannot edit or delete
- View only: Task name, Department, Planned/Actual dates, Status, Submitted by

---

## 💬 WhatsApp Feature (Super Admin Only)

**What it does:**
- When Super Admin clicks the WhatsApp button on a task
- It sends the task details to the assigned doer's WhatsApp number
- Message includes: Task name, Department, Frequency, Planned date

**Example message:**
```
Hello Swapan Kr Ghorai,

Pending Task Assignment

Task: B. Card-1 Machine Maintenance
Department: Yarn Division
Frequency: 2W
Planned Date: 30-03-2026

Please complete this task on time. Thank you!

— CheckList Maintenance System
```

**Requirements:**
- Doer must have WhatsApp number saved in database (user_type field must exist)
- Uses Doer's WhatsApp number from `doers` table

---

## 🗄️ DATABASE SETUP

### Add user_type column to doers table:

```sql
ALTER TABLE doers 
ADD COLUMN user_type TEXT CHECK (user_type IN ('Admin', 'Super Admin', 'User')) DEFAULT 'User';
```

### Update existing doers:

```sql
-- Set as Super Admin
UPDATE doers SET user_type = 'Super Admin' WHERE name = 'Swapan Kr Ghorai';

-- Set as User
UPDATE doers SET user_type = 'User' WHERE name = 'Other Person';
```

---

## 🎨 UI/UX FEATURES

✅ **Sidebar Menu:**
- Admin sees: Dashboard, Doers, Tasks, Master Schedule, Done List, Scoring
- User/Super Admin sees: My Tasks, Done List

✅ **Navbar Badges:**
- Admin badge: Red (#FF6B6B)
- Super Admin badge: Yellow (#FFD93D)
- User badge: Green (#6BCB77)

✅ **Mobile Responsive:**
- Sidebar collapses on mobile
- Toggle button in navbar
- Full responsive design

✅ **Task Status:**
- Overdue tasks show in red
- Pending tasks show countdown days
- Clean card-based layout

---

## 📱 MOBILE SUPPORT

- Responsive sidebar that hides on mobile
- Touch-friendly buttons
- All features work on tablets and phones
- Toggle menu button in top-left

---

## 🚀 GETTING STARTED

1. **Download** `CheckList-FIXED.html`
2. **Host** on any web server or open locally
3. **Login** with your credentials
4. **For Doers:** Add them in Doers section with User Type
5. **For Super Admin:** Set user_type = "Super Admin" for that doer

---

## ✨ KEY UPDATES

✅ User and Super Admin now see same "My Tasks" screen  
✅ WhatsApp button ONLY appears for Super Admin  
✅ Done List is read-only for both User and Super Admin  
✅ Same password "User@1234" for both User and Super Admin  
✅ Super Admin can send WhatsApp to assignee person  
✅ Removed duplicate Super Admin menu  
✅ Cleaner navigation structure  

---

## 🔒 SECURITY NOTES

- Admin credentials hardcoded (change in production)
- User/Super Admin login checks against doers table
- Role-based access control enforced
- No sensitive data in localStorage
- Use HTTPS in production

---

**Your CheckList system is now ready! 🎉**
