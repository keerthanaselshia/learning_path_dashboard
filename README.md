# ⚡ SkillForge - Learning Path Dashboard for Enhancing Skills

> A production-quality, personalized web application where learners pick a career goal (e.g., Full Stack Developer, Data Analyst, AI/ML Engineer, Cybersecurity Specialist, UI/UX Designer), take diagnostic skill assessments, and receive a dynamic, step-by-step roadmap that adapts to their ongoing progress.

---

## 🌟 Key & Unique Features

1. **Adaptive Path Engine**:
   - If a learner scores below 40% on an assessment, targeted **remedial revision modules** are automatically inserted into their timeline.
   - If they demonstrate advanced proficiency (>75%), foundational basics are skipped and advanced topics are unlocked immediately.

2. **🌌 Interactive "Skill Galaxy"**:
   - A custom HTML5 Canvas particle & node-graph visualizer representing your knowledge universe.
   - Mastered skills shine as **glowing electric-teal stars** with outer corona effects.
   - Unlocked topics appear as vibrant cyan planets.
   - Locked topics with unfulfilled prerequisites are dimmed in dark slate.
   - Clicking any node opens a modal displaying competency level, prerequisite requirements, and learning modules.

3. **⏱️ Daily Focus Mode (Pomodoro Timer)**:
   - Built-in timer (25 min standard, 50 min deep work, 5 min break) linked directly to the learner's current module.
   - Automatically records study sessions in the database upon completion and awards **1 XP per minute** studied.

4. **📈 Skill Gap Radar Matrix**:
   - Dynamic radar chart comparing the learner's verified capabilities against target role requirements.
   - Identifies major and minor competency gaps with color-coded alerts.

5. **🎯 Smart Goal Planner**:
   - Automatically distributes remaining curriculum modules across weeks leading up to the learner's target date.
   - Tracks if the student is **on track** or behind schedule and provides daily study recommendations.

6. **🏆 Gamification & Milestones**:
   - Experience Points (XP), dynamic learner levels, daily streak counter (🔥), and achievements:
     - `First Steps`, `7-Day Streak`, `Century Club`, `Speed Learner`, `Quiz Master`, `Perfectionist`, `Night Owl`, `Path Pioneer`.
   - Live community leaderboard ranked by total XP.

7. **⚙️ Full Admin Management Hub**:
   - Administrative panel with metrics: active learners, completion rates, and enrollment distribution.
   - CRUD management for Career Paths, Skills, Modules, and Assessment Quiz Questions.

8. **🎨 Modern Deep-Navy & Electric-Teal Design System**:
   - Custom glassmorphism layout with backdrop blur, responsive sidebar, smooth animations, and **Dark/Light theme toggle** (saved in localStorage).

---

## 🛠️ Tech Stack

- **Backend**: Java 17+ with Spring Boot 3.2.0
  - Spring Web (MVC & RESTful APIs)
  - Spring Data JPA (Hibernate ORM)
  - Spring Security 6 with dual authentication:
    - Session-based authentication for Thymeleaf UI
    - Stateless JWT authentication for REST API endpoints
  - Hibernate Bean Validation (Jakarta Validation)
  - Lombok
- **Database**: H2 in-memory relational database (pre-configured with full seed data; easily switchable to MySQL/PostgreSQL via `application.properties`)
- **Frontend**:
  - Thymeleaf Template Engine
  - Modern Custom CSS Design System (no generic Bootstrap look)
  - Vanilla JavaScript ES6+
  - Chart.js (Radar Charts, Study Hours Bar Chart)
  - HTML5 Canvas for the Skill Galaxy
- **Build Tool**: Maven

---

## 🚀 Getting Started & Execution

### Prerequisites
- **Java 17** or higher installed (`java -version`)
- **Maven 3.8+** installed (`mvn -v`)

### Running the Application

1. Open your terminal in the project directory:
   ```bash
   cd "c:\Users\keert\OneDrive\Attachments\JAVA MINIPROJECT"
   ```

2. Run the Spring Boot application:
   ```bash
   mvn spring-boot:run
   ```

3. Open your web browser and navigate to:
   ```
   http://localhost:8080
   ```

---

## 🔑 Default Seed Accounts & Credentials

The application includes an automated `DataLoader` that seeds 5 career paths, 30+ skills, 60+ modules, 50+ quiz questions, 8 badges, and pre-configured test users:

| Role | Username | Password | Notes |
| :--- | :--- | :--- | :--- |
| **Learner (Demo)** | `demo` | `demo123` | Enrolled in *Full Stack Developer*, has pre-populated module progress, quiz scores, active study sessions, and unlocked badges. |
| **Administrator** | `admin` | `admin123` | Access to `/admin` management hub, analytics, and curriculum authoring tools. |

*You can also register a brand new learner account at any time via `/register`.*

---

## 📂 Project Architecture

```
com.learningpath/
├── config/
│   ├── DataLoader.java             # Comprehensive seed data loader (5 paths, 30+ skills, 60+ modules, 50+ questions)
│   ├── SecurityConfig.java         # Dual filter chain: Session UI + Stateless REST JWT
│   └── WebConfig.java
├── controller/
│   ├── Web Controllers:
│   │   ├── PageController.java          # /, /login, /register
│   │   ├── DashboardController.java     # /dashboard
│   │   ├── AssessmentController.java    # /assessment, /assessment/{id}
│   │   ├── SkillGapController.java      # /skill-gap
│   │   ├── LearningPathController.java  # /learning-path
│   │   ├── SkillGalaxyController.java   # /skill-galaxy
│   │   ├── StudyTimerController.java    # /study-timer
│   │   ├── BadgePageController.java     # /badges
│   │   ├── ProfileController.java       # /profile
│   │   └── AdminController.java         # /admin, /admin/**
│   └── REST Controllers:
│       ├── AuthRestController.java          # /api/auth/**
│       ├── DashboardRestController.java     # /api/dashboard/**
│       ├── AssessmentRestController.java    # /api/assessment/**
│       ├── LearningPathRestController.java  # /api/learning-path/**
│       ├── StudySessionRestController.java  # /api/study-sessions/**
│       ├── SkillGalaxyRestController.java   # /api/skill-galaxy/**
│       ├── BadgeRestController.java         # /api/badges/**
│       ├── GoalPlannerRestController.java   # /api/goal-planner/**
│       └── AdminRestController.java         # /api/admin/**
├── dto/                             # 17 Data Transfer Objects
├── exception/
│   ├── GlobalExceptionHandler.java  # Centralized exception handling
│   └── ResourceNotFoundException.java
├── model/                           # 14 JPA Entities & Enums
│   ├── CareerPath.java
│   ├── Skill.java
│   ├── SkillPrerequisite.java
│   ├── Module.java
│   ├── Resource.java
│   ├── QuizQuestion.java
│   ├── QuizAttempt.java
│   ├── UserSkillLevel.java
│   ├── UserModuleProgress.java
│   ├── StudySession.java
│   ├── Badge.java
│   ├── UserBadge.java
│   ├── User.java
│   ├── Role.java (Enum)
│   ├── DifficultyLevel.java (Enum)
│   └── ResourceType.java (Enum)
├── repository/                      # 13 Spring Data JPA Repositories
├── security/
│   ├── CustomUserDetailsService.java
│   ├── JwtAuthenticationEntryPoint.java
│   ├── JwtAuthenticationFilter.java
│   └── JwtTokenProvider.java
└── service/
    ├── AuthService.java
    ├── CareerPathService.java
    ├── SkillService.java
    ├── ModuleService.java
    ├── QuizQuestionService.java
    ├── AssessmentService.java
    ├── LearningPathService.java
    ├── DashboardService.java
    ├── StudySessionService.java
    ├── BadgeService.java
    ├── GoalPlannerService.java
    └── AdminService.java
```

---

## 🌐 Database Console (H2)

When running in development mode, you can inspect the in-memory H2 database directly:
- **URL**: `http://localhost:8080/h2-console`
- **JDBC URL**: `jdbc:h2:mem:learningpathdb`
- **Username**: `sa`
- **Password**: *(leave blank)*

### Switching to MySQL (Optional)
To switch to MySQL, update `src/main/resources/application.properties`:
```properties
spring.datasource.url=jdbc:mysql://localhost:3306/learningpathdb?createDatabaseIfNotExist=true
spring.datasource.username=root
spring.datasource.password=yourpassword
spring.jpa.database-platform=org.hibernate.dialect.MySQLDialect
```
and add the MySQL connector dependency in `pom.xml`.

---

## 📄 License
This project is open-source and intended for educational and production reference.
