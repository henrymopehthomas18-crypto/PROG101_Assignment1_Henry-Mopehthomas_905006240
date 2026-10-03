Step 1: Start.
Step 2: Define constants: CRITICAL_LEVEL = 90, HIGH_LEVEL = 70, MEDIUM_LEVEL = 40, OVERDUE_DAYS = 3, TRUCK_CAPACITY = 5.
Step 3: Set criticalCount, highCount, mediumCount and lowCount to 0.
Step 4: Input totalReports.
Step 5: If totalReports is less than 1, display “invalid number of reports”. Otherwise(totalReports is 1 or more)
Step 6: Set i = 1.
Step 7: If i is greater than totalReports, go to Step 15.
Step 8: Input wardName, fillLevel, wasteType, isHazardous and daysSinceCollection.
Step 9: Call validateReport(). If it returns FALSE, display “Invalid data, re-enter report” and go back to Step 8.
Step 10: Call classifyPriority(fillLevel, isHazardous, daysSinceCollection) and store the result in priority.
Step 11: Increase the counter that matches priority (critical, high, medium or low) by 1.
Step 12: Display the confirmation: ward name and priority.
Step 13: Set i = i + 1.
Step 14: Go back to Step 7.
Step 15: Call calculateTrips(totalReports) and store the result in trips.
Step 16: Call displaySummary() to show the counts and the number of trips.
Step 17: Stop.
