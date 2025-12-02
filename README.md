# Security-Copilot-SCU-Optimiser
## Overview
This is deployment includes: 
- Azure Logic App
- Azure Workbook
Together, they enable the users to configure SCU usage schedules for each Security Copilot Capacity. The schedules are based on **Active Days** and **Active Hours**.
### How It Works
- During active hours on an active day, the number of SCUs is set to the maximum configured by the user.
- During inactive hours or inactive days, the number of SCUs is set to the minimum configured by the user.

**Special Feature**: User can set the minimum SCU count to zero.
- Since Security Copilot requires at least 1 SCU per active capacity, the Logic App:
  - stores the capacity's configuration.
  - deletes the capacity during inactive time if the minimum SCU is zero.
  - recreates the capacitiy during active time using the stored information.
- After recreation, the user must manually connect the capacity to one or more desired workspaces.
### Logic App Trigger
- Runs every hour at 5 minutes past.
- The schedules for each capacity are added to the capacities as tags. 
### Editing Deleted Capacities
If the user wants to alter the schedule of a deleted capacity before its next active window, this can be done by editing the stored configuration.

## Deployment Notes
- Connections must be configured after the deployment.
- The Azure Workbook is created inside the Logic App's resource group first, it needs to be moved to the Sentinel resource group.


[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FBeguemUysal%2FSecurity-Copilot-SCU-Optimiser%2Fmain%2Fsecuritycopilot_scu_optimiser.json?nocache=1)
