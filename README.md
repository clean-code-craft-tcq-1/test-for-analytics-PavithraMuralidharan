# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.

## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file
2. A valid csv file
3. Read access to the telemetrics file.
4. Threshold value to calculate the breach.
5. Tools/Library to generate pdf report.
6. Access to store PDF report in the server.
7. Recipient address to send notification.

(add more if needed)

### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | No | We do not test the efficiency of the pdf converter
Counting the breaches       | Yes | To check the count that has crossed threshold in a month.
Detecting trends            | Yes | To check continuous increasing of reading for 30 minutes
Notification utility        | Yes | To check whether the pdf has generated successfully.

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data
3. Write "Breach Count: {count}" to the PDF from the csv when the readings crosses the threshold in a month.
4. Write "No Breach Found" to the PDF when there is no readings crosses the threshold.
5. Write "Trends Recorded at {date and time}" to the PDF from the csv when the readings increases continuosly for 30 minutes.
6. Generate a "PDF Report" from csv data for every week.
7. Return "Report Generation Failure" when the pdf file is not generated for the week.
8. Return "true" when the notification is sent as expected. 
9. Return "false" when the notification is not sent as expected.
10. Return "File Not Found" when the file is not available in the server.
11. Return "Access Denied" when not able to access the file from the server.

(add more)

### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input        | Output                      | Faked/mocked part
|--------------------------|--------------|-----------------------------|---
Read input from server     | csv file     | internal data-structure     | Fake the server store
Validate input             | csv data     | valid / invalid             | None - it's a pure function
Notify report availability | pdf file and Recipients email | true/false               |Fake the Notification
Report inaccessible server | server credentials | Access denied to Server               | Fake the server store
Find minimum and maximum   |csv data | Minimum and Maximum value calculated with csv data               | None - it's a pure function
Detect trend               | csv data | date & time from csv data               | None - it's a pure function
Write to PDF               | csv data | pdf file                | Fake the PDF Generation
