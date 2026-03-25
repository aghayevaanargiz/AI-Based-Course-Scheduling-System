# AI-Based Classroom and Course Scheduling System

A constraint satisfaction problem (CSP) solution for university course timetabling, implementing backtracking search with Minimum Remaining Values (MRV) and Least Constraining Value (LCV) heuristics.

**Course:** CSCI3613 Artificial Intelligence  
**Institution:** ADA University, School of Information Technologies and Engineering  
**Semester:** Fall 2025  

---

## Project Overview

University course timetabling is a complex combinatorial problem involving the assignment of course sections to time slots, rooms, and instructors while satisfying numerous constraints. This project implements an AI-based scheduling system that generates feasible weekly timetables for the School of IT and Engineering.

**Problem Type:** Constraint Satisfaction Problem (CSP) with soft constraints

### Problem Structure

| Component | Description |
|-----------|-------------|
| **Course Sections** | Each section requires two weekly meetings on different days |
| **Variables** | Each meeting (2 per section) with domain of (day, time, room, instructor) |
| **Hard Constraints** | Must be satisfied for schedule to be valid |
| **Soft Constraints** | Preferences with penalty weights to be minimized |

---

## Data

### Dataset Construction

The dataset was constructed by collecting real structural information from the university's course offerings, including:

| Component | Source |
|-----------|--------|
| **Course Sections** | Actual courses offered by the School of IT and Engineering |
| **Instructors** | Real faculty members with their names and taught courses |
| **Room Capacities** | Actual classroom capacities in the university |
| **Instructor Availability** | Synthetically generated based on realistic academic schedules |
| **Workload Distributions** | Designed to reflect typical teaching loads |

### Data Collection Process

1. **Course Information**: Extracted from the university's course catalog, including course codes, titles, enrollment sizes, and instructor assignments

2. **Instructor Profiles**: Compiled actual faculty names and the courses they teach within the School of IT and Engineering

3. **Room Data**: Gathered real classroom capacities and availability patterns

4. **Availability Constraints**: Constructed realistic instructor time availability based on typical academic schedules and teaching responsibilities

5. **Workload Balancing**: Designed soft constraints to ensure fair distribution across instructors

### Data Format

The dataset is organized across multiple Excel files:

| File | Description |
|------|-------------|
| `courses.xlsx` | Course sections, enrollment numbers, required meetings |
| `instructors.xlsx` | Faculty names, taught courses, availability constraints |
| `rooms.xlsx` | Room capacities and types |
| `availability.xlsx` | Instructor time slot availability per day |

### Note

Instructor availability and certain workload distributions were synthetically generated to complete missing components while preserving realistic academic and operational constraints. The dataset is suitable for evaluating constraint-based scheduling methods and reflects the actual course structure of the School of IT and Engineering.

---

## Constraints

### Hard Constraints

| Constraint | Description |
|------------|-------------|
| Instructor Availability | Meetings only during instructor's available time slots |
| Room Capacity | Room must accommodate enrolled students |
| No Conflicts | No instructor or room assigned to two meetings simultaneously |
| Meeting Separation | Two meetings of same section on different days |
| Instructor Consistency | Same instructor for both meetings of a section |
| Master Course Limits | Maximum 2 master-level courses per day |
| Multi-Section Rules | Different instructors for different sections of same course |

### Soft Constraints

| Constraint | Penalty |
|------------|---------|
| Daily Workload | Penalty for exceeding max meetings per day per instructor |
| Weekly Workload | Penalty for exceeding max meetings per week per instructor |

---

## Methodology

### Algorithm

**Backtracking Search with Branch-and-Bound**

- Depth-first search exploring assignment space
- Early pruning based on accumulated soft constraint penalties
- Complete search guarantees finding optimal solution if one exists

### Heuristics

| Heuristic | Purpose | Impact |
|-----------|---------|--------|
| **MRV (Minimum Remaining Values)** | Select variable with smallest feasible domain first | Reduces branching factor by prioritizing constrained variables |
| **LCV (Least Constraining Value)** | Order values that leave most options for remaining variables | Preserves flexibility, reduces backtracking |

---

## Results

### Search Performance Comparison

| Configuration | Nodes Expanded | Max Depth | Solution Quality |
|--------------|----------------|-----------|------------------|
| Fixed Order Baseline | High | — | Satisfies hard constraints |
| MRV Only | Reduced | — | Improved efficiency |
| **MRV + LCV** | **8,398** | **Full depth** | **Optimal schedule** |

### Key Metrics

| Metric | Value |
|--------|-------|
| Total Variables | Number of meetings (2 × course sections) |
| Nodes Explored | 8,398 |
| Hard Constraints | 100% satisfied |
| Soft Constraint Penalty | Minimized |

### Workload Distribution

The generated schedule achieves balanced instructor workloads across days and weeks, demonstrating practical applicability.

---

## Repository Structure
