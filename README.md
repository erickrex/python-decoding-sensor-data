# Decoding Sensor Data with Python

- [Decoding Sensor Data with Python](#decoding-sensor-data-with-python)
  - [Status](#status)
  - [Overview](#overview)
  - [Installation](#installation)
    - [Verify Local Environment](#verify-local-environment)
    - [Windows](#windows)
    - [macOS](#macos)
    - [About pip](#about-pip)
  - [Verify Setup](#verify-setup)
  - [Previewing Your Work](#previewing-your-work)

## Status

This is a **Draft**.

## Overview

This project is design to be completed on [Pluralsight](https://pluralsight.com). To find out more see here: [https://www.pluralsight.com/product/projects](https://www.pluralsight.com/product/projects).

## Installation

### Verify Local Environment

### Windows

Open a command prompt or powershell and run the following commands, replacing 'project-root' with the path to the root folder of the project.

``` bash
> cd 'project-root'
> python -m venv venv
> venv\Scripts\activate.bat
> pip install -r requirements.txt
```

### macOS

Open a terminal and run the following commands, replacing 'project-root' with the path to the root folder of the project.

```bash
> cd 'project-root'
> python3 -m venv venv
> source venv/bin/activate
> pip install -r requirements.txt
```

*Note: If you've installed Python 3 using a method other than Homebrew, you might need to type `python` in the second command instead of `python3`.*

### About pip

`pip` updates frequently, but versions greater than 10.x.x should work with this project.

## Verify Setup

In order to verify that everything is setup correctly, run the following command from the project root.

```bash
pytest
```

You should see that all the tests are failing. This is good! We’ll be fixing these tests once we jump into the build step.

Every time you want to check your work locally you can type that command, and it will report the status of every task in the project.

## Previewing Your Work

You can preview your work by opening a terminal, changing to the project root, activating the virtual environment, and executing the appropriate python script. For example `python sensor/sensor.py`.



INSTRUCTIONS

Import os, glob, and csv

The dataset for this project is stored in several CSV files found in the dataset folder. It represents the data from a device with multiple sensors. The data was collected at random times over a period of days. The records include measurements of temperature, humidity, energy consumption, and particle count in the air over a given area. The data is collected over a period of 24 hours.

To start, open the file called load_data.py in the sensor folder.

At the top of the file, create three import statements for os, glob, and csv. These libraries will allow us to work with a collection of files.
2
Create a Function to Parse the Data

Create a function called load_sensor_data() that has no parameters. In the body of the load_sensor_data() function, create a variable called sensor_data and set it to an empty list.
3
Sensor Data File Management

Next, create a variable called sensor_files that is set to a call to the glob.glob() function.

Pass the glob function a single argument, a call to the os.path.join() function.

In turn pass os.path.join() three arguments: os.getcwd(), "datasets", and "*.csv".

Your statement should look like this:

    sensor_files = glob.glob(os.path.join(os.getcwd(), 'datasets', '*.csv'))

4
Read Data Files

The sensor_files object contains a list of file names, such as ['SENSOR_ROOM2', 'SENSOR_ROOM1']

To read the sensor data of these files, do the following:

    Create one for loop that loops through sensor_files using sensor_file as the iterator variable.

    In the body of this loop, use a with statement to open the sensor_file and set the alias to data_file.

    In the with body, set a variable called data_reader equal to csv.DictReader(). Pass in the current data_file as the first argument, and set the delimiter=',' as the second argument. The data_reader will contain a list of dictionaries with the sensor data.

5
Load Data Records

Now that you have access to the data in each file, the next step is to load each record into the sensor_data list.

Within the with, create a second for loop to data_file to get access to each record. Use row as your iterator variable.

Inside the body of the second for loop, append each row record to the sensor_data list (you created this list earlier in the Create a Function to Parse the Data task).

Finally, your function should return sensor_data (outside of all for loops, and the very end of the function).
6
Get Sensor Data with sensor_app

Let's set up the command line interface (CLI). Open the sensor_app.py file in the sensor directory of the project.

At the top of the file, from the load_data module, import the load_sensor_data function.

Then, below the two initial lines of code provided in the file

data = []
print("Sensor Data App")

Set the data list to load_sensor_data().

Print the length of the data list using the formatted string form str.format().

print("Loaded records: {}".format(len(data)))

To preview your app, open a terminal at the root of the project and run the following command:

python sensor/sensor_app.py

Sample output:

Sensor Data App
Loaded records: 2000

Remember, each data file contains 1000 records.

FYI: this project's tests will not validate your print() statements.
