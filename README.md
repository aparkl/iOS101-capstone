# Mosaic

## Table of Contents

1. [Overview](#Overview)
2. [Product Spec](#Product-Spec)
3. [Wireframes](#Wireframes)
4. [Schema](#Schema)

## Overview

### Description

**Mosaic** is an iOS-based task management application that helps users efficiently track and manage their time through tasks and sessions. Users can categorize tasks, monitor their daily productivity, and analyze their time spent on various responsibilities. By integrating time tracking with task organization, Mosaic provides a holistic view of how users spend their time and offers insights to improve productivity.

### App Evaluation

Category: Productivity / Self-Improvement

Mobile: Native mobile (iOS) – optimized for quick one-tap timers, notifications, and widgets (beyond MVP).

Story: Born from the struggle to balance task lists against real time spent—this app helps users become more mindful of where their minutes go.

Market: Students, freelancers, remote workers, and anyone looking to improve personal time management.

Habit: Stopwatch (MVP), streak bonuses, and daily summaries encourage users to open the app each day and log their work.

Scope: MVP is achievable in a short sprint: core CRUD + timer + basic dashboard. Future expansions can layer on analytics, tags, and cloud sync (will require serious tweaking to achieve).

## Product Spec

### 1. User Stories

**Required Must-have Stories**
- User can add, delete, and view tasks
- Each task includes a name, due date, category, and priority
- Stopwatch functionality for tracking task time (start/pause/stop)
- Categories can be created, viewed, and assigned to tasks
- Task list displays today's tasks, sorted by priority
- Persistent data storage with Core Data
- Dark mode support
- Delete tasks and categories with swipe gestures
- Universal tab bar with views: Today, Tasks, Add Task, Calendar, and Settings

**Optional Nice-to-have Stories**
- Task completion toggle and archiving
- Swipe gestures to view tasks by day (Calendar-style navigation)
- Estimated time vs. actual time analytics
- Recommendation system based on user behavior and ML
- Gamification (achievements, streaks, XP)
- Visual time reports and charts

### 2. Screen Archetypes

- **Today View**
  * View tasks due today
  * Start/stop stopwatch for each task

- **Task List**
  * View all tasks sorted by priority
  * Delete tasks via swipe

- **Add Task**
  * Form with fields: name, due date, priority, category
  * Save to database

- **Calendar View**
  * Select date and view corresponding tasks

- **Settings**
  * Toggle dark/light mode

- **Categories**
  * View, add, delete categories
  * Navigate to tasks under a specific category

### 3. Navigation

**Tab Navigation**
- Today
- Tasks
- Add Task
- Calendar
- Settings

**Flow Navigation**
- Add Task → Save Task → Return to Task List
- Category View → Add Category → Save → Return
- Task Button → Start Stopwatch → Update Time
- Calendar → Select Date → View Date-Specific Tasks

## Wireframes

![wireframe](https://github.com/user-attachments/assets/e4b66cd4-b57f-4dcf-bc14-a9a3ac48049f)


## Schema 

### Models

#### CDTask
| Property      | Type      | Description                      |
|---------------|-----------|----------------------------------|
| id            | UUID      | Unique ID                        |
| name          | String    | Name of the task                 |
| dueDate       | Date      | When the task is due             |
| priority      | Int16     | Priority level (0 = Low, 1 = Med, 2 = High) |
| completed     | Bool      | Whether task is completed        |
| createdAt     | Date      | Task creation date               |
| category      | CDCategory| Linked category                  |
| sessions      | Set<CDSession> | Associated work sessions   |

#### CDCategory
| Property  | Type   | Description               |
|-----------|--------|---------------------------|
| id        | UUID   | Unique ID                 |
| name      | String | Category name             |
| createdAt | Date   | Creation date             |
| tasks     | Set<CDTask> | Tasks under category  |

#### CDSession
| Property  | Type   | Description               |
|-----------|--------|---------------------------|
| id        | UUID   | Unique ID                 |
| startTime | Date   | Start of the session      |
| endTime   | Date?  | End of the session        |
| duration  | Double | Time in seconds           |
| task      | CDTask | Associated task           |

### Networking

N/A – Local Core Data is used. Future iterations may integrate with a backend for syncing and analytics.
