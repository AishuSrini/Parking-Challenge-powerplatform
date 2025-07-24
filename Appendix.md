# **Power Automate Expressions (Eastern Standard Time)**

Format parking request datetime from trigger:

```
formatDateTime(triggerOutputs()?['body/pc_parkingrequestdatetime'],'yyyy-MM-ddTHH:mm:ssZ')
```

# **Start of day in EST:**

```
formatDateTime(convertTimeZone(utcNow(),'UTC','Eastern Standard Time'),'yyyy-MM-ddT00:00:00Z')
```

# **End of day in EST:**

```
formatDateTime(convertTimeZone(utcNow(),'UTC','Eastern Standard Time'),'yyyy-MM-ddT23:59:59Z')
```

# **Dynamic filter for parking requests in a given EST day:**

```
pc_parkingrequestdatetime ge @{formatDateTime(convertTimeZone(utcNow(),'UTC','Eastern Standard Time'),'yyyy-MM-ddT00:00:00Z')} 
and 
pc_parkingrequestdatetime le @{formatDateTime(convertTimeZone(utcNow(),'UTC','Eastern Standard Time'),'yyyy-MM-ddT23:59:59Z')}
```

# **Power BI DAX Queries**
Date Dimension Table

'''
dimDate = ADDCOLUMNS(
    CALENDARAUTO(),
    "MonthID", MONTH([Date]),
    "Month", FORMAT([Date], "MMM"),
    "DayNumber", DAY([Date]),
    "DayName", FORMAT([Date], "dddd"),
    "DayID", WEEKDAY([Date], 2),
    "Year", YEAR([Date]),
    "Today", TODAY(),
    // Add a SchoolYear column that adjusts the year based on the month
    "SchoolYear", IF(
        MONTH([Date]) >= 9,
        YEAR([Date])+1,
        YEAR([Date])
    ),
    "SchoolMonthID", if (MONTH([Date]) >= 9,
        Month([Date])-9,
        Month([Date])+3
    ),
    "Report Refresh", Now() //We'll use this to display the report refresh date
)
'''

# **Key Measures & Calculated Columns**

'''
// Create a new date-only column from InspectionDateTime
InspectionDate = 
DATE(
    YEAR('Parking Inspections'[InspectionDateTime]),
    MONTH('Parking Inspections'[InspectionDateTime]),
    DAY('Parking Inspections'[InspectionDateTime])
)

// Check if this inspection has an associated Parking Request
isRequested = 
IF(
    NOT(ISBLANK('Parking Inspections'[ParkingRequest])), 
    TRUE(),  // Has associated request, thus permitted
    FALSE()  // No request, thus not permitted
)
'''
// Measures

'''
Total Inspections = 
COUNTROWS('Parking Inspections')

Total Requests = 
CALCULATE(
    COUNTROWS('Parking Inspections'),
    'Parking Inspections'[isRequested] = TRUE()
)
'''
'''
% Inspections with Valid Parking Requests = 
DIVIDE(
    [Total Requests],
    [Total Inspections],
    0
)
'''
