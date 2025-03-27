# REAL-TIME-DASHBOARD
 COMPANY: CODTECH IT SOLUTIONS PVT.LTD

 NAME: Shivam Mishra

 INTERNID: CT12PFA

 DOMAIN: POWER BI

 DURATION: 8 WEEKS

 MENTOR: NEELA SANTOSH

Here’s a detailed explanation of your real-time data streaming project in Power BI Service using an API:

---

## **Real-Time Data Streaming in Power BI Using API**

### **Project Overview**
This project involves real-time data streaming into Microsoft Power BI Service using PowerShell and an API. It simulates continuous data generation for humidity and air quality index (AQI) in Jaipur city, sending this data to a Power BI dataset. The data is then visualized dynamically on a Power BI dashboard.

---

### **Components Involved**
1. **Power BI Streaming Dataset**
2. **PowerShell Script for Data Generation**
3. **Power BI Dashboard for Visualization**

---

### **1. Power BI Streaming Dataset Setup**
- A streaming dataset was created in Power BI Service to receive real-time data.
- The dataset includes the following fields:
  - `Humidity`: Represents the humidity level (1-100).
  - `AQI`: Air Quality Index value (150-280).
  - `DateTime`: Timestamp of the reading.
  - `City`: Fixed as “Jaipur”.

- The dataset is configured to accept POST requests through an API endpoint.

---

### **2. PowerShell Script for Data Simulation**
The PowerShell script continuously sends random values of humidity and AQI to Power BI Service using the `Invoke-RestMethod` command.

#### **Code Breakdown:**
- The `endpoint` variable holds the Power BI API URL.
- The script runs an infinite `while($true)` loop to generate continuous data.
- `Get-Random` is used to generate random humidity (1-100) and AQI (150-280).
- The current timestamp (`DateTime`) is captured using `Get-Date`.
- The data is formatted as JSON (`$payload`).
- `Invoke-RestMethod` sends the JSON data as a POST request to Power BI Service.
- `Start-Sleep 1` ensures a 1-second delay between each data entry.

#### **Code Used:**
```powershell
$endpoint = "https://api.powerbi.com/beta/{YourDatasetID}/rows?key={YourAPIKey}"

while($true) {
    $x = Get-Random -Minimum 1 -Maximum 100
    $y = (Get-Date).ToUniversalTime().ToString("yyyy-MM-ddTHH:mm:ss")
    $z = Get-Random -Minimum 150 -Maximum 280
    $payload = @{
        "Humidity" = $x
        "City" = "Jaipur"
        "DateTime" = $y
        "AQI" = $z
    }
    Invoke-RestMethod -Method Post -Uri "$endpoint" -Body (ConvertTo-Json @($payload))
    Start-Sleep 1
}
```
This script continuously feeds new data points to Power BI every second.

---

### **3. Power BI Dashboard for Visualization**
After setting up the dataset, a dashboard was created in Power BI Service to visualize the real-time data.

#### **Visualization Elements:**
1. **Humidity Gauge** – Displays the latest humidity level.
2. **AQI Gauge** – Shows the latest AQI value.
3. **Line Chart for Humidity** – Plots humidity levels over time.
4. **Bar Chart for AQI** – Tracks AQI trends over time.

These visualizations update automatically as new data arrives.

---

### **Project Outcome**
- **Real-time Data Streaming**: The dashboard updates every second with fresh data.
- **Dynamic Monitoring**: The changing humidity and AQI levels allow live tracking.
- **Power BI API Utilization**: Demonstrates how Power BI can integrate with external data sources.

---

### **Possible Enhancements**
- Integrating real IoT sensor data instead of random values.
- Adding more environmental parameters (temperature, pollution levels).
- Implementing alerts for critical AQI or humidity levels.

---

### **Conclusion**
This project successfully demonstrates how Power BI can handle real-time data streaming via an API using PowerShell. The dashboard provides dynamic insights into humidity and AQI levels in Jaipur, making it a useful model for real-time environmental monitoring.

