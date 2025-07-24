# 🚗 **Power Platform Parking Challenge Solution**
## 🌟 **Overview**

This repository contains my submission for the Microsoft Power Up Challenge—a real-world scenario addressing parking management at Contoso High School, built using the Microsoft Power Platform suite. The solution delivers robust parking request management, daily inspections, automated notifications, and actionable analytics, all within a scalable, extensible low-code framework.
## 🏫 **Problem Statement**

**Contoso High School** faced increasing complaints about parking availability from both staff and visitors. To address this, the leadership team required a solution to:

* Allow daily parking requests from staff and visitors

* Enable a parking inspector to log parked vehicles at 5PM daily

* Provide insights to reduce unauthorized parking and optimize parking management
# 💡 **Solution Components**
# **1. Dataverse Data Model**

Three key tables (entities) were created:

* **Vehicle Table:** Holds all registered vehicles, with columns for VehicleName, Make, Model, VehicleOwnerEmail, and VehicleImage.

![Vehicle Table: ](https://github.com/AishuSrini/Parking-Challenge-powerplatform/blob/main/vehicle%20table.png)

* **Parking Request Table:** Captures each parking request (ParkingRequestName, Vehicle, ParkingRequestDateTime).
  
![Parking Request Table: ](https://github.com/AishuSrini/Parking-Challenge-powerplatform/blob/main/parking%20request%20table.png)

* **Parking Inspection Table:** Logs daily inspections (ParkingInspectionName, InspectionDateTime, Vehicle, ParkingRequest).
 
![Parking Inspection Table: ](https://github.com/AishuSrini/Parking-Challenge-powerplatform/blob/main/parking%20inspection%20table.png)

# **Forms:**
Each table includes a custom form for data entry and updates:

* **Vehicle Form:** Includes subgrids for related Parking Requests and Inspections.
  
![Vehicle Table Form: ](https://github.com/AishuSrini/Parking-Challenge-powerplatform/blob/main/Table%20Forms%20Screenshots/New%20vehicle%20form.png)

* **Parking Request Form:** Ties each request to a vehicle and date/time.
  
![Parking Request Table Form: ](https://github.com/AishuSrini/Parking-Challenge-powerplatform/blob/main/Table%20Forms%20Screenshots/New%20parking%20Request%20form.png)

* **Parking Inspection Form:** Connects each inspection to both the vehicle and (optionally) a valid parking request.

![Parking Inspection Table Form: ](https://github.com/AishuSrini/Parking-Challenge-powerplatform/blob/main/Table%20Forms%20Screenshots/new%20parking%20inspection%20form.png)

# **Views:**

* **Active Vehicles:** Quick overview for admins (VehicleName, Make, Model, Owner).

![Active Vehicles View: ](https://github.com/AishuSrini/Parking-Challenge-powerplatform/blob/main/Table%20views%20Screenshots/Active%20vehicle%20view.png)

* **Active Parking Requests/Today:** Review and filter requests (by name, date/time, vehicle; filtered for today).

![Active Parking Request View: ](https://github.com/AishuSrini/Parking-Challenge-powerplatform/blob/main/Table%20views%20Screenshots/Active%20Parking%20Request%20view.png)

**Active Parking Requests Today View:** 

![Active Parking Request Today View: ](https://github.com/AishuSrini/Parking-Challenge-powerplatform/blob/main/Table%20views%20Screenshots/Active%20parking%20request%20Today%20view.png)

* **Active Parking Inspections/Today:** See all inspections for the current day, with related vehicle and request info.
  
![Active Parking Inspections View: ](https://github.com/AishuSrini/Parking-Challenge-powerplatform/blob/main/Table%20views%20Screenshots/Active%20parking%20inspection%20view.png)

**Active Parking Inspections Today View:**

![Active Parking Inspections Today View: ](https://github.com/AishuSrini/Parking-Challenge-powerplatform/blob/main/Table%20views%20Screenshots/Active%20parking%20inspection%20Today%20view.png)

Data was populated using the provided CSV templates, following the prescribed order (Vehicle → Parking Request → Parking Inspection) and with US datetime formatting as required.

# **2. Model-Driven App**
The model-driven app serves as the administrative hub for the solution:

* Manage vehicles, parking requests, and inspections via unified navigation

* Create and review parking requests on behalf of staff/visitors

* Access relational data (vehicle → requests/inspections)

* Perform CRUD operations across all tables with built-in security and audit trails

**Forms and views** from the Dataverse model are embedded, ensuring a consistent, modern, and streamlined admin experience.

**Model Driven App -Active Parking Inspections page:**

![Model Driven App -Active Parking Inspections page: ](https://github.com/AishuSrini/Parking-Challenge-powerplatform/blob/main/model-driven%20app%20screenshot/Activ%20parking%20inspections.png)

# **3. Canvas App (Inspector App)**
A tablet-optimized canvas app enables field inspectors to efficiently log daily inspections:

**Screens:**

* **Home:** Easy navigation to ‘Review’ or ‘New Inspection’ screens
  
![Home Screen](https://github.com/AishuSrini/Parking-Challenge-powerplatform/blob/main/canvas%20app%20screenshot/home%20screen.png)

* **Review:** Gallery of today’s inspections (Inspection, Vehicle, DateTime, Make, Model, ParkingRequest, ParkingRequestDateTime)
  
![Review Screen](https://github.com/AishuSrini/Parking-Challenge-powerplatform/blob/main/canvas%20app%20screenshot/Review%20Screen.png)

* **New Inspection:** Form for logging an inspection, pre-populated with the current time; vehicle selection; quick creation of new vehicles if needed
  
![New Inspection Screen](https://github.com/AishuSrini/Parking-Challenge-powerplatform/blob/main/canvas%20app%20screenshot/New%20inspection%20Screen.png)

* **New Vehicle:** Capture and register vehicles not previously seen; post-submission navigation ensures updated inspection data
![New Vehicle Screen](https://github.com/AishuSrini/Parking-Challenge-powerplatform/blob/main/canvas%20app%20screenshot/New%20Vehicle%20Screen.png)

**Modern controls** and clear headers are used throughout for usability.

# **4. Power Automate Cloud Flow**
**Parking Request Notification:**

* Automated cloud flow sends a personalized email to vehicle owners upon approval of their parking request.

* Dynamic email fields: vehicle name, request ID, with the school signature.

* Advanced logic uses **Power Fx** and flow expressions to:

+ **Enforce 5PM cutoff** (no valid requests after inspection)

+ **Respect parking lot capacity** (limit to 15 spots per day; overflows handled accordingly)

Admins are advised to disable the flow when bulk uploading requests to avoid excessive emails.
![Power AUtomate Workflow](https://github.com/AishuSrini/Parking-Challenge-powerplatform/blob/main/PowerAutomate%20Screenshot/parking%20notification%20workflow.png)

# **5. Power BI Report**
The Power BI analytics solution is designed for actionable insight and executive review:

- **Three Pages:**

   -   **Home:** Navigation buttons to Filters and Parking Review
![Home Page](https://github.com/AishuSrini/Parking-Challenge-powerplatform/blob/main/powerBI%20screenshot/Home%20page.png)

   -   **Filters:** Slicers for vehicle make/model, calendar, and day of week;   changes reflect dynamically across all report pages

![Filters Page](https://github.com/AishuSrini/Parking-Challenge-powerplatform/blob/main/powerBI%20screenshot/Filter%20page.png)

   -   **Parking Review:** Key cards (Total Inspections, % Valid Requests), bar charts (inspection outcomes over time), matrices (per-vehicle analytics), and direct links to underlying inspection records in the model-driven app

![Parking Review Page](https://github.com/AishuSrini/Parking-Challenge-powerplatform/blob/main/powerBI%20screenshot/Parking%20Review%20page.png)

* **Data Model:**

   + Integrates Parking Inspections, Vehicles, and a calculated Date dimension using DAX (see [Appendix 1] for formula).

   + Valid inspections are defined by the relationship between inspections and parking requests.

   + Measures include Total Inspections, Total Requests, % Inspections with Valid Requests.

* **Cross-Page Filtering & Navigation:**

   + Selecting a filter (vehicle or date) updates all linked metrics and visuals across the report.

   + Navigation buttons and links provide a seamless analytic experience.
# 📚 **Appendix**

All key Power Automate expressions and Power BI DAX queries for this solution are documented in [APPENDIX.md](https://github.com/AishuSrini/Parking-Challenge-powerplatform/blob/main/Appendix.md)

# 🤖 **Demo:**

**Watch a Demo Video:**
[Watch the demo on YouTube] https://youtu.be/3sR2cVcJAeo

# 🚦 **Solution Impact**
* **End-to-end process automation:** From request to inspection and reporting.

* **Data-driven management:** Immediate visibility into compliance, occupancy, and unauthorized use.

* **Extensible framework:** Ready to adapt for broader organizational needs (e.g., multi-site, predictive analytics, integration with physical access systems).

* **User-centric design:** Intuitive forms, mobile-friendly inspector workflow, and clear, actionable reports.

# 📂 **Files Included**
* ParkingChallengeDemo_1_0_0_2_managed.zip — Managed Power Platform solution (import via Power Platform Solutions)

* Parking Inspection Report.pbix — Power BI report (open in Power BI Desktop)

* /screenshots/ — Key visuals of the apps and reports

# 📝 **How to Use**
1.Import the managed solution into your Power Platform environment.

2.Launch the model-driven app for administration.

3.Deploy the canvas app on a tablet for daily inspections.

4.Configure email for the automated flow (for real notifications).

5.Open the Power BI report to analyze parking data and trends.

6.(Optional) Extend with sample data or your own customizations.

# **🌱 How Would I Extend This Solution?**
* Enable self-service portals for staff/visitor parking requests.

* Integrate with real-time campus access control and license plate recognition via AI Builder.

* Expand analytics to include forecasted demand and suggest optimal parking assignments.

* Adapt solution for business campuses, hospitals, or event venues with multiple lots and access tiers.

# **🤝 Contributing**
Contributions are welcome!
If you have suggestions for new features or enhancements, please open an issue or submit a pull request.
When contributing, please follow these steps:

1.Fork the repository

2.Create a new branch for your feature/fix

3.Commit your changes with clear messages

4.Open a pull request describing your changes

# **📝 License**
This project is provided under the MIT License.
You are free to use, modify, and distribute this solution for educational and non-commercial purposes.

Developed as part of the Microsoft Power Up Program – Pathfinder (Power Platform). For learning and demonstration only. No confidential data included.
