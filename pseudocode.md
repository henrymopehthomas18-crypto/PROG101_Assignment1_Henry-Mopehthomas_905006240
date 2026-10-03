# Pseudocode – CleanFreetown


CONSTANT CRITICAL_LEVEL = 90
CONSTANT HIGH_LEVEL = 70
CONSTANT MEDIUM_LEVEL = 40
CONSTANT OVERDUE_DAYS = 3
CONSTANT TRUCK_CAPACITY = 5

FUNCTION validateReport(wardName, fillLevel, daysSince) RETURNS BOOLEAN
    IF wardName = "" THEN RETURN FALSE
    IF fillLevel < 0 OR fillLevel > 100 THEN RETURN FALSE
    IF daysSince < 0 THEN RETURN FALSE
    RETURN TRUE
END FUNCTION

FUNCTION classifyPriority(fillLevel, isHazardous, daysSince) RETURNS STRING
    IF fillLevel >= CRITICAL_LEVEL OR isHazardous = TRUE THEN
        RETURN "CRITICAL"
    ELSE IF fillLevel >= HIGH_LEVEL AND daysSince >= OVERDUE_DAYS THEN
        RETURN "HIGH"
    ELSE IF fillLevel >= MEDIUM_LEVEL THEN
        RETURN "MEDIUM"
    ELSE
        RETURN "LOW"
    END IF
END FUNCTION

FUNCTION calculateTrips(totalReports) RETURNS INTEGER
    trips <- totalReports DIV TRUCK_CAPACITY
    IF totalReports MOD TRUCK_CAPACITY > 0 THEN
        trips <- trips + 1
    END IF
    RETURN trips
END FUNCTION

PROCEDURE displaySummary(critical, high, medium, low, trips)
    OUTPUT "===== CLEANFREETOWN SUMMARY ====="
    OUTPUT "CRITICAL: ", critical
    OUTPUT "HIGH:     ", high
    OUTPUT "MEDIUM:   ", medium
    OUTPUT "LOW:      ", low
    OUTPUT "Total valid reports: ", critical + high + medium + low
    OUTPUT "Truck trips needed: ", trips
END PROCEDURE

MAIN
    criticalCount <- 0
    highCount <- 0
    mediumCount <- 0
    lowCount <- 0

    OUTPUT "Enter number of reports:"
    INPUT totalReports

    IF totalReports < 1 THEN
        OUTPUT "Invalid number of reports"
        STOP
    END IF

    FOR i <- 1 TO totalReports
        REPEAT
            INPUT wardName, fillLevel, wasteType, isHazardous, daysSince
            isValid <- validateReport(wardName, fillLevel, daysSince)
            IF isValid = FALSE THEN
                OUTPUT "Invalid data, re-enter report"
            END IF
        UNTIL isValid = TRUE

        priority <- classifyPriority(fillLevel, isHazardous, daysSince)

        CASE priority OF
            "CRITICAL" : criticalCount <- criticalCount + 1
            "HIGH"     : highCount <- highCount + 1
            "MEDIUM"   : mediumCount <- mediumCount + 1
            "LOW"      : lowCount <- lowCount + 1
        END CASE

        OUTPUT wardName, " -> ", priority
    END FOR

    trips <- calculateTrips(totalReports)
    displaySummary(criticalCount, highCount, mediumCount, lowCount, trips)
END MAIN
