6.1 Scenario A – Six Reports (including one invalid entry)
No.	Ward	Fill %	Hazardous	Days	Valid?	Priority	Reason
1	Kroo Bay	95	No	1	Yes	CRITICAL	95 >= 90
2	Wellington	75	No	4	Yes	HIGH	75 >= 70 AND 4 >= 3
3	Lumley	45	No	1	Yes	MEDIUM	45 >= 40
4	Goderich	20	No	0	Yes	LOW	Below all limits
5a	Murray Town	130	No	2	No	Rejected	Fill level > 100; user must re-enter
5b	Congo Town	30	Yes	2	Yes	CRITICAL	Hazardous = TRUE
6	Murray Town	55	No	1	Yes	MEDIUM	55 >= 40

Expected screen output for Scenario A:
Kroo Bay -> CRITICAL
Wellington -> HIGH
Lumley -> MEDIUM
Goderich -> LOW
Invalid data, re-enter report
Congo Town -> CRITICAL
Murray Town -> MEDIUM
 
===== CLEANFREETOWN SUMMARY =====
CRITICAL: 2
HIGH:     1
MEDIUM:   2
LOW:      1
Total valid reports: 6
Truck trips needed: 2

Trip calculation check: 6 DIV 5 = 1 and 6 MOD 5 = 1, which is greater than 0, so trips = 1 + 1 = 2.
6.2 Scenario B – Boundary Tests for classifyPriority()
Fill %	Hazardous	Days	Expected Priority	Reason
90	No	0	CRITICAL	Exactly on CRITICAL_LEVEL
89	No	5	HIGH	Below 90; 89 >= 70 and 5 >= 3
70	No	2	MEDIUM	70 >= 70 but days < 3, so HIGH fails; 70 >= 40
70	No	3	HIGH	Both HIGH conditions true
40	No	0	MEDIUM	Exactly on MEDIUM_LEVEL
39	No	9	LOW	Below 40
10	Yes	0	CRITICAL	Hazardous overrides low fill level
