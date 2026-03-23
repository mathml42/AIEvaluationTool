### **Set Up Test Data Management System (TDMS)**
---
Access the web-based UI for managing test data and users.
This module provides comprehensive CRUD (Create, Read, Update, Delete) operations for test cases within the TDMS (Test Data Management System) application. For user manual [click here](../docs/TDMS_Documentation.pdf)

#### 5.2.1 **Backend Setup**

**Step 1: Configure Database**

Update `src/app/TDMS/back-end/database/config.json` with your MariaDB credentials else sqlite will works by defaults.
**Configure the database:**
      
   **For SQLite (default, recommended for development):**
   ```json
   {
     "db": {
       "engine_type": "sqlite",
       "file": "TDMS.db"
     }
   }
   ```
   
   **For MariaDB (production):**
   ```json
   {
     "db": {
       "engine_type": "mariadb",
       "host": "localhost",
       "port": 3306,
       "user": "your_username",
       "password": "your_password",
       "database": "tdms_db"
     }
   }
   ```

#### Step 2: Start the Application

**Terminal 1 - Start Backend Server:**
```bash
cd src/app/TDMS/back-end
source venv/bin/activate
python main.py
```

The backend will start on `http://localhost:8000`

![back End running](../screenshots/backEnd.png)

#### 5.2.2 Frontend Setup

1. **Navigate to the frontend directory:**
   ```bash
   cd src/app/TDMS/front-end
   ```

2. **Install Node.js dependencies:**
   ```bash
   npm install
   ```


**Terminal 2 - Start Frontend Development Server:**
```bash
cd src/app/TDMS/front-end
npm run dev
```

The frontend will start on `http://localhost:8080` (or another port if 8080 is busy)

![Front End Running](../screenshots/frontEnd.png)

#### 5.2.3 Access the Application

1. Open your web browser
2. Navigate to `http://localhost:8080` (or the port shown in the terminal)
3. You should see the login page

![TDMS Home page](../screenshots/tdms_home.png)

#### **Access TDMS**

Use these login credentials:

| Role | Username | Password |
|------|----------|----------|
| Admin | `admin` | `admin123` |
| Manager | `manager` | `manager123` |
| Curator | `curator` | `curator123` |
| Viewer | `viewer` | `viewer123` |

---

