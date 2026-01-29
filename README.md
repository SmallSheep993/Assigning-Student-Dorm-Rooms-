# Assigning Student Dorm Rooms

This project implements a fair and constraint-aware dormitory room assignment system.  
It matches students to rooms and potential roommates while strictly enforcing hard constraints such as:

- accessibility requirements  
- separation of undergraduate and graduate housing  
- individual affordability limits  

On top of these constraints, the system optimizes multiple student preferences, including:

- preferred hall and room type  
- preferred amenities (e.g. proximity to food, downtown, services)  
- preferred price range  
- preferred roommate compatibility  

## Policy

Students are prioritized by academic seniority (credits earned).  
Higher-credit students are assigned first, reflecting a transparent, rule-based priority system similar to real university housing.

Accessibility needs and eligibility rules are always enforced, so no student is placed in an invalid room.

This design intentionally favors senior students while still ensuring meaningful satisfaction for all groups. Differences in outcomes are a policy choice, not an error.

## Algorithm

The assignment runs in two stages:

1. **Maximum-Weight Roommate Matching**  
   Students are paired using a graph matching algorithm that maximizes compatibility based on factors like schedule, accessibility, and preference similarity.

2. **Constrained Deferred Acceptance (DA)**  
   Individuals and roommate pairs propose to valid rooms in order of preference.  
   Rooms accept applicants based on:
   1. credit-based priority tier  
   2. random tie-breaking  
   3. preference score  

This produces a stable matching where no student-room pair would mutually prefer to deviate.

## Results and Evaluation

Across multiple datasets:

- ~65–79% of students receive a room in their preferred price range  
- ~64–77% satisfy private bathroom preference  
- ~68–79% satisfy laundry availability  
- average composite preference score ≈ 11–12  

Senior and graduate students achieve higher preference satisfaction by design, while underclassmen still receive housing in large numbers due to cohort size.

All accessibility and eligibility constraints are always satisfied.

## Tradeoffs

**Strengths**
- High roommate compatibility before room assignment  
- Stable, transparent, and easily adjustable policy  
- Strong overall preference satisfaction under strict constraints  

**Limitations**
- Deterministic seniority priority reduces satisfaction for first-year students  
- Limited affordable capacity lowers outcomes for lower-credit tiers  

Possible improvements include reserved capacity for early-year students or weighted randomness within priority tiers.

## Output

The algorithm outputs matches in the format:

(student_id, [hall_name, building_id, room_id])

Unassigned students are reported as:

(student_id, nan)

Results are saved as CSV files for each dataset.  
If randomness is used, multiple runs can be generated to show variability.

## Tech Stack

- Python  
- Pandas / NumPy  
- Graph-based matching + Deferred Acceptance  

## Summary

This system demonstrates how explicit policy choices combined with advanced matching algorithms can balance fairness, stability, and preference satisfaction under real-world housing constraints.
