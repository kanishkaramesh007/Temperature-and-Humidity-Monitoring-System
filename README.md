# Temperature-and-Humidity-Monitoring-System
To develop an Android application to monitor temperature and humidity values and display warning messages based on predefined limits.

# TEMPERATURE AND HUMIDITY MONITORING SYSTEM

## 1. AIM
To develop an Android application for monitoring temperature and humidity levels, displaying the measured values, and generating alerts when the readings exceed predefined threshold limits.

## 2. SOFTWARE REQUIREMENTS
- Android Studio
- Java Programming Language
- XML for UI Design
- Android SDK
- Android Emulator or Android Smartphone

**Hardware Requirements (Optional):**
- Raspberry Pi
- DHT11 or DHT22 Temperature and Humidity Sensor
- Wi-Fi connectivity
- Jumper wires and breadboard

## 3. THEORY
A Temperature and Humidity Monitoring System is designed to measure and monitor the surrounding environmental conditions.

Temperature indicates the degree of hotness or coldness of the environment, while humidity represents the amount of water vapour present in the air.

The Android application provides a user-friendly interface to enter or receive temperature and humidity readings and display them on the mobile screen.

The application compares the readings with predefined threshold values and displays warning messages whenever the measured values exceed the specified limits.

A DHT11 or DHT22 sensor can be interfaced with a Raspberry Pi to obtain real-time temperature and humidity readings. The Raspberry Pi can transmit the sensor data to the Android application through Wi-Fi communication.

## 4. PROCEDURE
1. Open Android Studio and create a new project.
2. Select an Empty Views Activity and choose Java as the programming language.
3. Provide the application name as **Temperature and Humidity Monitoring System**.
4. Design the user interface using XML.
5. Add input fields to enter temperature and humidity values.
6. Add a Monitor button to process the entered readings.
7. Add TextViews to display the temperature, humidity and monitoring status.
8. Write Java code to retrieve the entered values.
9. Compare the readings with predefined threshold values.
10. Display suitable warning messages if the readings exceed the limits.
11. Run the application using an Android emulator or smartphone.
12. Verify the application by entering different temperature and humidity values.

## 5. ALGORITHM
1. Start the application.
2. Initialize the temperature and humidity input fields.
3. Enter the temperature and humidity readings.
4. Click the Monitor button.
5. Read the entered values.
6. Check whether the temperature exceeds the predefined limit (35°C).
7. Check whether the humidity exceeds the predefined limit (70%).
8. If either value exceeds its limit, display a warning message.
9. Otherwise, display a normal environmental condition message.
10. Display the readings on the application screen.
11. Stop.
# XML CODE
      <?xml version="1.0" encoding="utf-8"?>
    <ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <LinearLayout
        android:orientation="vertical"
        android:gravity="center"
        android:padding="24dp"
        android:layout_width="match_parent"
        android:layout_height="wrap_content">

        <TextView
            android:text="TEMPERATURE AND HUMIDITY MONITOR"
            android:textSize="22sp"
            android:textStyle="bold"
            android:gravity="center"
            android:padding="15dp"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"/>

        <TextView
            android:text="Enter Sensor Readings"
            android:textSize="18sp"
            android:textStyle="bold"
            android:padding="12dp"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"/>

        <EditText
            android:id="@+id/etTemperature"
            android:hint="Temperature in Celsius"
            android:inputType="numberDecimal|numberSigned"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"/>

        <EditText
            android:id="@+id/etHumidity"
            android:hint="Humidity in Percentage"
            android:inputType="numberDecimal"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"/>

        <Button
            android:id="@+id/btnCheck"
            android:text="CHECK READINGS"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"/>

        <TextView
            android:id="@+id/tvTemperature"
            android:text="Temperature: -- °C"
            android:textSize="20sp"
            android:padding="12dp"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"/>

        <TextView
            android:id="@+id/tvHumidity"
            android:text="Humidity: -- %"
            android:textSize="20sp"
            android:padding="12dp"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"/>

        <TextView
            android:id="@+id/tvStatus"
            android:text="System Status: Waiting for input"
            android:textSize="18sp"
            android:textStyle="bold"
            android:gravity="center"
            android:padding="15dp"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"/>

    </LinearLayout>
    </ScrollView>
# JAVA PROGRAM
     package com.example.temperaturemonitoring;

    import android.app.Activity;
    import android.os.Bundle;
    import android.widget.*;

     public class MainActivity extends Activity {

    EditText etTemperature, etHumidity;

    Button btnCheck;

    TextView tvTemperature, tvHumidity, tvStatus;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        etTemperature = findViewById(R.id.etTemperature);
        etHumidity = findViewById(R.id.etHumidity);

        btnCheck = findViewById(R.id.btnCheck);

        tvTemperature = findViewById(R.id.tvTemperature);
        tvHumidity = findViewById(R.id.tvHumidity);
        tvStatus = findViewById(R.id.tvStatus);

        btnCheck.setOnClickListener(v -> checkReadings());
    }

    void checkReadings() {

        String tempInput =
                etTemperature.getText().toString().trim();

        String humidityInput =
                etHumidity.getText().toString().trim();

        if (tempInput.isEmpty() ||
                humidityInput.isEmpty()) {

            Toast.makeText(this,
                    "Please enter both readings",
                    Toast.LENGTH_SHORT).show();
            return;
        }

        try {

            double temperature =
                    Double.parseDouble(tempInput);

            double humidity =
                    Double.parseDouble(humidityInput);

            if (temperature < -50 ||
                    temperature > 100 ||
                    humidity < 0 ||
                    humidity > 100) {

                Toast.makeText(this,
                        "Enter valid sensor readings",
                        Toast.LENGTH_SHORT).show();
                return;
            }

            tvTemperature.setText(
                    "Temperature: " + temperature + " °C");

            tvHumidity.setText(
                    "Humidity: " + humidity + " %");

            if (temperature > 35 || humidity > 70) {

                tvStatus.setText(
                        "WARNING: High Temperature or Humidity!");

            } else {

                tvStatus.setText(
                        "System Status: NORMAL");

            }

        } catch (NumberFormatException e) {

            Toast.makeText(this,
                    "Invalid input",
                    Toast.LENGTH_SHORT).show();
        }
    }
    }
## 6. EXPECTED OUTPUT
<img width="1600" height="803" alt="image" src="https://github.com/user-attachments/assets/e535a8d9-d853-4944-95e1-74a854b9dcb6" />

## 7. APPLICATION FEATURES
- User-friendly Android interface.
- Displays temperature and humidity readings.
- Compares readings with predefined threshold values.
- Generates warning messages for abnormal conditions.
- Supports manual entry of sensor readings.
- Can be extended for real-time monitoring using Raspberry Pi and DHT11/DHT22 sensors.
- Can be enhanced with graphical representation and periodic data logging.

## 8. RESULT
The Temperature and Humidity Monitoring System Android application was developed successfully. The application accepts temperature and humidity readings, displays the values and generates alerts when the readings exceed the predefined threshold limits.

## 9. CONCLUSION
The developed application provides a simple method for monitoring environmental temperature and humidity conditions. It demonstrates Android application development using Java and XML. The system can be further enhanced by interfacing a DHT11/DHT22 sensor with Raspberry Pi to enable real-time environmental monitoring through wireless communication.
