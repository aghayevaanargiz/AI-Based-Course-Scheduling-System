# AI-Based Classroom and Course Scheduling System

A constraint satisfaction problem (CSP) solution for university course timetabling, implementing backtracking search with Minimum Remaining Values (MRV) and Least Constraining Value (LCV) heuristics.

**Course:** CSCI3613 Artificial Intelligence  
**Institution:** ADA University, School of Information Technologies and Engineering  
**Semester:** Fall 2025  

---

## Project Overview

University course timetabling is a complex combinatorial problem involving the assignment of course sections to time slots, rooms, and instructors while satisfying numerous constraints. This project implements an AI-based scheduling system that generates feasible weekly timetables for the School of IT and Engineering.

**Problem Type:** Constraint Satisfaction Problem (CSP) with hard and soft constraints

### Problem Statistics

| Metric | Value |
|--------|-------|
| Course Sections | 41 |
| Instructors | 37 (professors and instructors) |
| Rooms | 14 |
| Time Slots | 7 slots/day × 5 days = 35 slots |
| Meeting Variables | 82 (2 per section) |
| Average Domain Size | 184 values per variable |

---

## Dataset

The dataset was constructed from actual university course offerings and faculty information, with realistic availability constraints.

### Data Files

| Sheet | Description | Records |
|-------|-------------|---------|
| **Courses** | Course sections with enrollment counts | 41 |
| **InstructorCourses** | Instructor-to-course assignments | 36 |
| **Hard** | Instructor unavailability constraints | 90 |
| **Soft** | Instructor teaching preferences (1-5) | 150+ |
| **RoomSeatingCapacity** | Classroom capacities | 14 |

### Course Distribution

| Department | Sections |
|------------|----------|
| CSCI (Computer Science) | 26 |
| INFT (Information Technology) | 10 |
| SITE (School Core) | 2 |
| MATH (Mathematics) | 6 |

### Instructor Categories

| Type | Weekly Limit |
|------|--------------|
| Professors (PROF) | 6 meetings/week |
| Instructors (INST) | 6 meetings/week |

### Room Capacities

| Capacity Range | Rooms |
|----------------|-------|
| 15-20 seats | 5 |
| 25-35 seats | 5 |
| 40-55 seats | 4 |

---

## Constraints

### Hard Constraints (Must Satisfy)

| Constraint | Description |
|------------|-------------|
| Instructor Availability | Meetings only during available time slots (from Hard sheet) |
| Room Capacity | Room capacity must meet or exceed enrollment |
| No Conflicts | No instructor or room assigned to two meetings simultaneously |
| Meeting Separation | Two meetings of same section on different days |
| Instructor Consistency | Same instructor for both meetings of a section |
| Master Course Limit | Maximum 2 master-level meetings per day |
| Two-Instructor Rule | Courses with ≥3 sections use ≤2 distinct instructors |

### Soft Constraints (Minimized)

| Constraint | Weight | Limit |
|------------|--------|-------|
| Daily Workload Excess | 5 | Max 2 meetings/day/instructor |
| Weekly Workload Excess | 3 | Max 6 meetings/week/instructor |

---

## Algorithms Implemented

### 1. Baseline Solver (Fixed Order)
- Simple backtracking with fixed variable order
- Branch-and-bound pruning
- Serves as performance baseline

### 2. MRV Solver
- Minimum Remaining Values heuristic
- Selects most constrained variable first
- Reduces search space by prioritizing variables with fewest options

### 3. MRV + LCV Solver
- MRV for variable selection
- Least Constraining Value for value ordering
- Values that leave most options for remaining variables are tried first

---

## Results

### Performance Comparison

| Solver | Nodes Expanded | Max Depth | Avg Branching | Max Branching | Penalty | Time (s) |
|--------|---------------|-----------|---------------|---------------|---------|----------|
| Fixed Order Baseline | — | 82 | — | — | 44 | 300.07 |
| MRV Only | 8,062 | 82 | 82.19 | 249 | 37 | 300.01 |
| **MRV + LCV** | **8,398** | **82** | **86.11** | **254** | **12** | **300.07** |

### Key Findings

| Finding | Insight |
|---------|---------|
| MRV reduces search complexity | 8,062 nodes explored with MRV vs significantly more without |
| MRV + LCV achieves lowest penalty | Penalty reduced from 44 to 12 (73% improvement) |
| Both heuristics reach full depth | All 82 meeting variables assigned successfully |
| Soft constraints effectively minimized | Daily and weekly workload limits respected where possible |

---

## Requirements
pandas>=1.3.0
openpyxl>=3.0.0
numpy>=1.21.0
