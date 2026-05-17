## Overview

TeamMatch is a web application designed to help instructors create balanced student teams for course projects. Instead of manually grouping students or relying on random assignment, TeamMatch uses student profile data, skills, experience levels, availability, and instructor-defined constraints to generate more balanced and explainable team assignments.

The system is built for classroom environments where instructors need to manage multiple courses, large student rosters, weekly progress updates, and team health concerns. TeamMatch gives instructors a structured way to form teams, review team results, monitor contributions, and identify students or teams that may need support.

## Key Features

- Student profile collection for skills, experience, availability, and preferences
- Instructor course management and team formation constraints
- Automated team generation using weighted scoring
- Team balance calculations based on skill distribution, schedule overlap, and experience levels
- Match run tracking with status updates such as `PENDING` and `COMPLETED`
- Instructor review and override support
- Weekly student check-ins for contribution tracking
- AI-assisted team health reports and recommendations
- Persistent storage for courses, students, teams, match runs, check-ins, and analytics data

## Tech Stack

### Frontend
- React
- Next.js
- Vercel deployment
- Browser-based student and instructor interface

### Backend
- FastAPI
- Python
- SQLAlchemy ORM
- Azure App Service
- REST API architecture
- Background processing for team formation

### Database
- Azure PostgreSQL Flexible Server
- Relational schema for users, courses, students, teams, match runs, check-ins, and analytics records
- Indexed tables for faster team lookup, course queries, and match run recovery

### AI Integration
- Anthropic Claude API
- Structured JSON request and response payloads
- AI-generated team health reports
- Instructor recommendations based on team check-in patterns

## System Architecture

TeamMatch follows a cloud-based client-server architecture.

Students and instructors interact with the application through the frontend in their web browsers. The frontend sends HTTPS requests to the FastAPI backend, which acts as the main business logic layer. The backend handles validation, authentication, API routing, database operations, team formation, and AI analytics requests.

Persistent data is stored in Azure PostgreSQL Flexible Server. This includes student profiles, courses, teams, match runs, weekly check-ins, and analytics data. For AI analytics, the backend sends structured team information to the Anthropic Claude API. Claude then returns instructor-facing summaries, at-risk student indicators, recommendations, and action plans.

## Core Workflow

1. Students submit their profile information, including skills, experience, availability, and preferences.
2. Instructors configure course constraints such as team size, skill requirements, and balancing priorities.
3. An instructor triggers a new match run.
4. The backend creates a `MatchRun` record with an initial `PENDING` status.
5. The matching process evaluates possible team combinations using weighted scoring.
6. Generated teams are stored in the database.
7. The match run status updates to `COMPLETED`.
8. Instructors review the generated teams and can make adjustments if needed.
9. Students submit weekly check-ins after teams are formed.
10. AI analytics generate team health reports based on check-in history and team data.

## Matching Logic

The team formation system evaluates students across multiple dimensions, including:

- Skill balance
- Schedule overlap
- Experience distribution
- Role preference compatibility
- Instructor-defined constraints

Each possible team grouping receives a weighted score. The goal is not just to create teams quickly, but to create teams that are balanced, explainable, and easier for instructors to review.

The matching process is designed to be deterministic and instructor-controlled. AI is used to assist with interpretation, reporting, and explanation, while the core team formation logic remains rule-based and reproducible.

## AI Analytics

TeamMatch uses AI to help instructors understand team health after teams have been created. The backend sends structured JSON data to Claude, including team scores, member information, skills, experience levels, and weekly check-in trends.

Claude returns a structured report with four main sections:

- Team summary
- At-risk students
- Instructor recommendations
- Action plan

This helps instructors identify struggling teams earlier and intervene before problems become more serious.

## Database Responsibilities

The database layer stores and organizes the main application entities, including:

- Users
- Courses
- Student profiles
- Skills
- Availability
- Constraints
- Match runs
- Teams
- Team members
- Weekly check-ins
- Analytics payloads

The schema was designed to support both the team formation workflow and long-term tracking of student contributions. SQLAlchemy models define relationships between courses, students, match runs, teams, and check-ins.

## My Contributions

My main role focused on the database and backend structure of TeamMatch. I helped design the PostgreSQL schema, implemented SQLAlchemy ORM models and relationships, and worked on API routes related to student data and team formation support.

Some of my contributions included:

- Designing a relational schema with around 10 core tables
- Creating SQLAlchemy models and relationships
- Seeding demo data with multiple courses and over 100 students
- Working on `/students/` API functionality
- Supporting match run recovery for stuck or incomplete runs
- Improving database indexing and connection handling
- Helping connect backend logic to persistent database records

## Example API Endpoints

### Student Profile

```http
POST /students/profile
