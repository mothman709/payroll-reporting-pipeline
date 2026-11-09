# Payroll Reporting Pipeline

An Excel workbook that uses Power Query to turn three biweekly exports into payroll hours, gross pay, follow-up lists for managers, and one combined follow-up list with a row per employee.

The case study is on my portfolio at https://othmanjournal.com/portfolio/payroll-reporting-pipeline.html

## What it does

Every pay period the workbook reads three files from three folders:

- an attendance export with employee punches
- a schedule export with scheduled shifts
- an HRIS export with employee details and pay rates

It matches each punch to the employee's scheduled shift, adjusts punch times, calculates regular and overtime hours and gross pay, and produces these sheets:

| Sheet | What it shows |
|---|---|
| Follow_Up_List | One row per employee with counts of missed punches, exceptions, absences and overtime weeks, overtime hours, a total, and the dates of each issue |
| Employee_Summary | Days worked, total hours, regular hours, overtime hours, pay rate and gross pay |
| Weekly_Hours | Hours per employee per Monday to Sunday week, regular and overtime |
| Overtime_List | Employee weeks over 44 hours |
| Exception_List | Punches that differ from the schedule by more than 15 minutes, or that have no schedule |
| Missed_Punch_List | Shifts with a check in or check out missing |
| Absence_List | Scheduled shifts with no punch at all |

## Rules built into the workbook

- A punch within 15 minutes of the scheduled start or end time counts as the scheduled time.
- A punch further off than that is paid at the punched time and goes on the Exception_List.
- A missing check in or check out gets no hours and goes on the Missed_Punch_List.
- Overtime is calculated per Monday to Sunday week. Hours over 44 are paid at 1.5 times the regular rate.
- There is no meal break deduction and no averaging agreement.
- Absences are found by expanding each employee's schedule across the 14 days of the pay period and keeping the shifts with no matching punch.

## Folder layout

```
Payroll_Pipeline.xlsx
Source_Attendance/    attendance export for the current pay period
Source_HRIS/          HRIS export
Source_Schedule/      schedule export
Attendance_Punch_Export_20261005_20261018.xlsx    previous pay period
Screenshots/
```

## Updating for a new pay period

1. Replace the file in Source_Attendance with the new attendance export. Update the HRIS and schedule files if they changed.
2. In Excel, click Data, then Refresh All.

The first time you open the workbook on a different computer, the three queries need to be pointed at the folders. In Power Query, open each Source query and change the folder path.

## Tools

Excel and Power Query.
