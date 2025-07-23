# 🚗 **Power Platform Parking Challenge Solution**
# 🌟**Overview**

This repository contains my submission for the Microsoft Power Up Challenge—a real-world scenario addressing parking management at Contoso High School, built using the Microsoft Power Platform suite. The solution delivers robust parking request management, daily inspections, automated notifications, and actionable analytics, all within a scalable, extensible low-code framework.
# 📄 **Project Brief**

Contoso High School faced increasing complaints about parking availability from both staff and visitors. To address this, the leadership team required a solution to:

1.Allow daily parking requests from staff and visitors

2.Enable a parking inspector to log parked vehicles at 5PM daily

3.Provide insights to reduce unauthorized parking and optimize parking management
# **🛠️ Solution Components**
**1. Dataverse Data Model**

Three key tables (entities) were created:

**Vehicle:** Holds all registered vehicles, with columns for VehicleName, Make, Model, VehicleOwnerEmail, and VehicleImage.

**Parking Request:** Captures each parking request (ParkingRequestName, Vehicle, ParkingRequestDateTime).

**Parking Inspection:** Logs daily inspections (ParkingInspectionName, InspectionDateTime, Vehicle, ParkingRequest).

# **Forms:**
Each table includes a custom form for data entry and updates:

**Vehicle Form:** Includes subgrids for related Parking Requests and Inspections.

**Parking Request Form:** Ties each request to a vehicle and date/time.

**Parking Inspection Form:** Connects each inspection to both the vehicle and (optionally) a valid parking request.

# **Views:**

**Active Vehicles:** Quick overview for admins (VehicleName, Make, Model, Owner).

**Active Parking Requests/Today:** Review and filter requests (by name, date/time, vehicle; filtered for today).

**Active Parking Inspections/Today:** See all inspections for the current day, with related vehicle and request info.

Data was populated using the provided CSV templates, following the prescribed order (Vehicle → Parking Request → Parking Inspection) and with US datetime formatting as required.

