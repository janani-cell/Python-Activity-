# Python Case Studies (41-50)
PITAMBARA JANANI ACHAR
CSD-2
ROL NO.:26001491

This repository contains Python solutions, algorithms, pseudocode, test cases, and problem statements for Case Studies 41 through 50. These projects focus on advanced data structures in Python, primarily utilizing **nested lists**, **tuples**, **matrices**, and **dictionary structures** to solve real-world analytical problems.

---

## 📋 Table of Contents

- [Overview of Case Studies](#-overview-of-case-studies)
- [Case Studies Summary](#-case-studies-summary)
  - [Case 41: Nested List Classroom Occupancy Analysis](#case-41-nested-list-classroom-occupancy-analysis)
  - [Case 42: Student Marks Matrix Analysis](#case-42-student-marks-matrix-analysis)
  - [Case 43: Multi-Branch Sales Matrix Comparison](#case-43-multi-branch-sales-matrix-comparison)
  - [Case 44: Hospital Ward Occupancy Monitoring](#case-44-hospital-ward-occupancy-monitoring)
  - [Case 45: Weekly Electricity Consumption Matrix](#case-45-weekly-electricity-consumption-matrix)
  - [Case 46: Inventory Matrix Reconciliation](#case-46-inventory-matrix-reconciliation)
  - [Case 47: Sports Tournament Ranking System](#case-47-sports-tournament-ranking-system)
  - [Case 48: Tuple-Based Employee Shift Conflict Detection](#case-48-tuple-based-employee-shift-conflict-detection)
  - [Case 49: Tuple-Based Product Catalogue Audit](#case-49-tuple-based-product-catalogue-audit)
  - [Case 50: Tuple-Based Route Distance Analysis](#case-50-tuple-based-route-distance-analysis)
- [How to Run](#-how-to-run)

---

## 📚 Overview of Case Studies

| Case No. | Title | Core Data Structures | Key Logic / Algorithm |
| :--- | :--- | :--- | :--- |
| **Case 41** | Classroom Occupancy Analysis | Nested Lists | Duplicate Detection, Occupancy Counting |
| **Case 42** | Student Marks Matrix Analysis | 2D Matrix (Nested Lists) | Row/Column Calculations, Max Search |
| **Case 43** | Multi-Branch Sales Matrix | 3D Nested Lists | Multi-level Aggregation, Performance Comparison |
| **Case 44** | Hospital Ward Occupancy Monitoring | 2D Matrix & Lists | Threshold Validation, Capacity Violation Detection |
| **Case 45** | Weekly Electricity Consumption Matrix | 2D Matrix | Limit Checking, Highest Aggregation |
| **Case 46** | Inventory Matrix Reconciliation | 2D Matrix | Matrix Column Summing, Target Reconciliation |
| **Case 47** | Sports Tournament Ranking System | Dictionaries & Tuples | Tie-breaking Logic, Custom Multi-key Sorting |
| **Case 48** | Employee Shift Conflict Detection | List of Tuples | Interval Overlap Detection Algorithm ($start_1 < end_2 \land start_2 < end_1$) |
| **Case 49** | Product Catalogue Audit | List of Tuples | Record Validation, Inventory Reorder Level Check |
| **Case 50** | Route Distance Analysis | List of Coordinate Tuples | Euclidean Distance Formula Calculation |

---

## 🛠 Case Studies Summary

### Case 41: Nested List Classroom Occupancy Analysis
* **Problem:** Represent multiple classrooms and seating positions using nested lists to allocate students, detect duplicate seat assignments, preserve reserved seats, and count vacant seats.
* **Code:**
```python
classrooms = [
    ["S101", "S102", None, "S104"],
    ["S105", "S106", "S101", None],
    ["Reserved", "S108", None, "S110"]
]
reserved_seats = 1
assigned_students = []
duplicates = []
occupied_seats = 0
total_seats = 0

for classroom in classrooms:
    for seat in classroom:
        total_seats += 1
        if seat == "Reserved":
            continue
        elif seat is not None:
            if seat in assigned_students:
                duplicates.append(seat)
            else:
                assigned_students.append(seat)
                occupied_seats += 1

vacant_seats = total_seats - occupied_seats - reserved_seats

print("CLASSROOM OCCUPANCY REPORT")
print("--------------------------")
print("Total Seats:", total_seats)
print("Occupied Seats:", occupied_seats)
print("Reserved Seats:", reserved_seats)
print("Vacant Seats:", vacant_seats)
print("Duplicate Student Assignments:", duplicates)
```

---

### Case 42: Student Marks Matrix Analysis
* **Problem:** Analyze a 2D matrix of student marks across subjects. Calculate individual student aggregates/averages, subject-wise averages, detect top performers, and flag low-performing subjects (average < 70).
* **Code:**
```python
students = ["Student 1", "Student 2", "Student 3"]
subjects = ["Python", "Maths", "English"]
marks = [
    [85, 90, 80],
    [70, 75, 65],
    [95, 92, 88]
]

totals = []
print("STUDENT MARKS REPORT")
print("--------------------")
for i in range(len(students)):
    total = sum(marks[i])
    average = total / len(subjects)
    totals.append(total)
    print(students[i], "Total:", total, "Average:", round(average, 2))

print("\nSUBJECT AVERAGES")
for j in range(len(subjects)):
    total = sum(marks[i][j] for i in range(len(students)))
    average = total / len(students)
    print(subjects[j], "Average:", round(average, 2))
    if average < 70:
        print("Low-performing subject:", subjects[j])

top_index = totals.index(max(totals))
print("\nTop Performer:", students[top_index])
print("Highest Total Marks:", totals[top_index])
```

---

### Case 43: Multi-Branch Sales Matrix Comparison
* **Problem:** Store 3D nested lists representing sales data across branches, products, and days. Calculate product and branch totals, and determine the top branch and top-performing product per branch.
* **Code:**
```python
branches = ["Branch 1", "Branch 2", "Branch 3"]
products = ["Laptop", "Mobile", "Tablet"]
sales = [
    [[10, 12, 8], [15, 10, 5], [6, 8, 4]],
    [[12, 10, 9], [10, 14, 6], [8, 7, 5]],
    [[15, 12, 10], [8, 9, 7], [5, 6, 4]]
]

branch_totals = []
for i in range(len(branches)):
    print("\n" + branches[i])
    total_branch = 0
    for j in range(len(products)):
        total_product = sum(sales[i][j])
        total_branch += total_product
        print(products[j], "Total Sales:", total_product)
    branch_totals.append(total_branch)
    print("Total Branch Sales:", total_branch)
    
    best_product_index = 0
    for j in range(1, len(products)):
        if sum(sales[i][j]) > sum(sales[i][best_product_index]):
            best_product_index = j
    print("Best Performing Product:", products[best_product_index])

best_branch_index = branch_totals.index(max(branch_totals))
print("\nBest Performing Branch:", branches[best_branch_index])
print("Highest Branch Sales:", branch_totals[best_branch_index])
```

---

### Case 44: Hospital Ward Occupancy Monitoring
* **Problem:** Analyze daily bed occupancy using a matrix. Calculate occupancy percentage relative to ward capacities, flag capacity overruns, and find peak demand days.
* **Code:**
```python
wards = ["Ward A", "Ward B", "Ward C"]
capacities = [30, 20, 25]
days = ["Mon", "Tue", "Wed"]
occupancy = [
    [25, 29, 31],
    [15, 18, 17],
    [20, 22, 24]
]

daily_totals = [0] * len(days)
for i in range(len(wards)):
    for j in range(len(days)):
        occupied = occupancy[i][j]
        daily_totals[j] += occupied
        utilization = (occupied / capacities[i]) * 100
        print(wards[i], days[j], "Utilization:", round(utilization, 1), "%")
        if occupied > capacities[i]:
            print("CAPACITY VIOLATION:", wards[i], days[j])

peak_index = daily_totals.index(max(daily_totals))
print("Daily Totals:", daily_totals)
print("Peak-Demand Day:", days[peak_index])
```

---

### Case 45: Weekly Electricity Consumption Matrix
* **Problem:** Track daily appliance consumption (kWh) over 7 days. Identify highest-consuming appliances and warn when combined daily usage surpasses predefined thresholds (e.g., $5.0 \text{ kWh}$).
* **Code:**
```python
appliances = ["Fan", "Light", "Computer"]
usage = [
    [1.2, 1.1, 1.3, 1.2, 1.1, 1.4, 1.0],
    [0.8, 0.7, 0.8, 0.9, 0.7, 0.8, 0.9],
    [2.5, 2.8, 3.0, 2.6, 2.9, 3.2, 2.7]
]
daily_limit = 5.0
appliance_totals = []

for i in range(len(appliances)):
    total = sum(usage[i])
    appliance_totals.append(total)
    print(appliances[i], "weekly consumption:", round(total, 2), "kWh")

for day in range(7):
    daily_total = sum(usage[appliance][day] for appliance in range(len(appliances)))
    print("Day", day + 1, "total:", round(daily_total, 2), "kWh")
    if daily_total > daily_limit:
        print("Warning: daily limit exceeded")

highest = appliance_totals.index(max(appliance_totals))
print("Highest-consuming appliance:", appliances[highest])
```

---

### Case 46: Inventory Matrix Reconciliation
* **Problem:** Compare product stock levels stored across multiple warehouse locations against target inventory to identify surplus, shortage, or exact match conditions.
* **Code:**
```python
warehouses = ["Warehouse A", "Warehouse B", "Warehouse C"]
products = ["Pens", "Books", "Bags"]
stock = [
    [100, 40, 15],
    [80, 60, 20],
    [70, 50, 10]
]
targets = [300, 180, 50]

for j in range(len(products)):
    total = sum(stock[i][j] for i in range(len(warehouses)))
    difference = total - targets[j]
    print(products[j], "total stock:", total, "target:", targets[j])
    if difference < 0:
        print("Shortage:", -difference)
    elif difference > 0:
        print("Surplus:", difference)
    else:
        print("Stock exactly meets target")
```

---

### Case 47: Sports Tournament Ranking System
* **Problem:** Process raw match tuples `(team1, score1, team2, score2)` to compute overall points ($3$ for win, $1$ for draw, $0$ for loss) and goal differences, then rank teams using key sorting.
* **Code:**
```python
teams = ["Tigers", "Eagles", "Lions"]
matches = [
    ("Tigers", 3, "Eagles", 1),
    ("Lions", 2, "Tigers", 2),
    ("Eagles", 2, "Lions", 0)
]

stats = {team: {"points": 0, "for": 0, "against": 0} for team in teams}

for t1, s1, t2, s2 in matches:
    stats[t1]["for"] += s1
    stats[t1]["against"] += s2
    stats[t2]["for"] += s2
    stats[t2]["against"] += s1
    if s1 > s2:
        stats[t1]["points"] += 3
    elif s2 > s1:
        stats[t2]["points"] += 3
    else:
        stats[t1]["points"] += 1
        stats[t2]["points"] += 1

ranking = sorted(
    teams,
    key=lambda team: (
        stats[team]["points"],
        stats[team]["for"] - stats[team]["against"]
    ),
    reverse=True
)

print("Rank  Team    Points  Difference")
for rank, team in enumerate(ranking, start=1):
    difference = stats[team]["for"] - stats[team]["against"]
    print(rank, team, stats[team]["points"], difference)
```

---

### Case 48: Tuple-Based Employee Shift Conflict Detection
* **Problem:** Compare employee shifts stored as tuples `(name, start_hour, end_hour)` to detect time overlap conflicts assigned to the same employee.
* **Code:**
```python
shifts = [
    ("Asha", 9, 12),
    ("Ravi", 10, 14),
    ("Asha", 11, 13),
    ("Asha", 13, 16),
    ("Ravi", 15, 17)
]
conflict_found = False

for i in range(len(shifts)):
    name1, start1, end1 = shifts[i]
    for j in range(i + 1, len(shifts)):
        name2, start2, end2 = shifts[j]
        if name1 == name2 and start1 < end2 and start2 < end1:
            print("Conflict:", shifts[i], "and", shifts[j])
            conflict_found = True

if not conflict_found:
    print("No shift conflicts found.")
```

---

### Case 49: Tuple-Based Product Catalogue Audit
* **Problem:** Validate product tuples `(id, price, quantity)`. Check for invalid data (empty IDs or negative prices/quantities), calculate total stock values, and flag reorder requirements.
* **Code:**
```python
products = [
    ("P101", 25.0, 30),
    ("P102", 120.0, 6),
    ("P103", -5.0, 12),
    ("P104", 50.0, 0)
]
reorder_level = 10

for product in products:
    product_id, price, quantity = product
    if product_id == "" or price < 0 or quantity < 0:
        print(product_id, "INVALID RECORD")
        continue
    value = price * quantity
    print(product_id, "inventory value:", round(value, 2))
    if quantity < reorder_level:
        print(product_id, "requires replenishment")
```

---

### Case 50: Tuple-Based Route Distance Analysis
* **Problem:** Take coordinate point tuples $(x, y)$ along a path, compute Euclidean distances between successive pairs using $d = \sqrt{(x_2-x_1)^2 + (y_2-y_1)^2}$, and locate the longest segment.
* **Code:**
```python
from math import sqrt

points = [
    (0, 0),
    (3, 4),
    (9, 4),
    (10, 12)
]
longest_distance = -1
longest_segment = None

for i in range(len(points) - 1):
    x1, y1 = points[i]
    x2, y2 = points[i + 1]
    dx = x2 - x1
    dy = y2 - y1
    distance = sqrt(dx ** 2 + dy ** 2)
    print("Segment", points[i], "to", points[i + 1], "distance:", round(distance, 2))
    if distance > longest_distance:
        longest_distance = distance
        longest_segment = (points[i], points[i + 1])

print("Longest segment:", longest_segment)
print("Longest distance:", round(longest_distance, 2))
```


