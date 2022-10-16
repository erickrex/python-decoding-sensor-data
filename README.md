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

## HOME DATA CLASS

Create HouseInfo Class

To start, open the file called house_info.py in the sensor folder.

Create a class called HouseInfo. Next, create a HouseInfo class constructor with two parameters, self and data.

In the body of the constructor, assign the data input parameter to a class attribute with the same name. Hint: class attributes are prefixed with self.
2
Create Method to Select Data by Area

Still in the HouseInfo class, create a method called get_data_by_area() with three parameters, self, field, and rec_area. The rec_area parameter should have a default value of 0, which translates to all records. The purpose of this method is to filter the data using rec_area as the key, and field as the value.

Note: The valid field values are the column names of the data files in the datasets folder.

In the body of the get_data_by_area() method, create a variable called field_data and set it to an empty list.
3
Filter Data Records by Area

On a new line in the get_data_by_area method, create a for loop to iterate over self.data. Use record as your iterator variable.

Note: The self.data class variable is a list of dictionaries. The dictionary keys are equal to the columns names in the data files. e.g. when the field input parameter is set to "id" then, the record[field] value corresponds to the "id" column values. In this method, the rec_area variable maps to 'area' column values.

In the body of the for loop, select records according to the following control structures:

    Create an if statement that is true when rec_area is equal to 0
        In the body of the if, append to the record[field] values to the field_data list.

    Create an else if statement that is true when rec_area is equal to record['area'] value. In order to compare the rec_area integer object to the record['area'] string object, the later needs to be converted to an integer using the int() constructor.
        In the body of the elif, append to the record[field] values to the field_data list.

Finally, your method should return field_data (outside of the for loop, and the very end of the method).
4
Create Method to Select Data by Date

Still in the HouseInfo class, create another method called get_data_by_date() with three parameters, self, field, and rec_date. The rec_date parameter should have the current date as its default value.

You can get the current date using the date module. At the top of the file, import date and datetime from the datetime module. See date information and datetime information.

In the body of the get_data_by_date() method, create a variable called field_data and set it to an empty list.
5
Filter Data Records by Date

On a new line in the get_data_by_date() method, create a for loop to iterate over self.data. Use record as your iterator variable.

Note: In this method, the rec_date input parameter maps to the 'date' column's values.

Now, in the body of the for loop, create an if statement that's true when the current record's date is equal to rec_date.

    In order to compare the record['date'] string to rec_date, which is a date object, convert rec_date to string using the strftime() method method. strftime() takes the argument "%m/%d/%y", which is the format of your dates.

In the body of the if statement, append to field_data the dictionary values whose record key is equal to field.

Finally, your method should return field_data (outside of the for loop, and at the very end of the method).
6
Get HouseInfo Data by Area with sensor_app

Open the sensor_app.py file in the sensor directory. At the top of the file, from the house_info module, import the HouseInfo.

At the bottom of the file, create an instance of the HouseInfo class, and assign it to a variable named house_info. Pass the HouseInfo constructor data as its argument.

Create a variable called test_area and set it to 1

Next, create another variable called recs and set it to the get_data_by_area() method of the house_info object. The get_data_by_area() method should take "id" as the first argument, and rec_area=test_area as the second argument.

Print the length of the recs list using the formatted string:


print("\nHouse sensor records for area {} = {}".format(test_area, len(recs)))



To preview your app, open a terminal at the root of the project and run the following command:

python sensor/sensor_app.py

Sample output including previous tasks:

Sensor Data App
Loaded records: 2000
House sensor records for area 1 = 1000

FYI: the app will not validate your print() statements.
7
Get HouseInfo Data by Date with sensor_app

Still in the sensor_app file, at the top of the file, from the datetime module, import the date and datetime.

At the bottom of the file, create a variable called test_date and set it to the call of datetime.strptime() which takes "5/9/20" as the first argument, and "%m/%d/%y" as the second argument.

Next, set the recs variable to the return value of get_data_by_date() method of the house_info object. The method takes "id" as the first argument, and rec_date=test_date as the second argument.

Print the test_date using the strftime() passing "%m/%d/%y" as the input parameter, and the length of the recs list using the formatted string:

print("\nHouse sensor records for date: {} = {}".format(test_date.strftime("%m/%d/%y"), len(recs)))

To preview your app, open a terminal at the root of the project and run the following command:

python sensor/sensor_app.py

Sample output including previous tasks:

Sensor Data App
Loaded records: 2000

House sensor records for area 1 = 1000
House sensor records for date: 05/09/20 = 20

FYI: the app will not validate your print() statements.

## Analyze Temperature Data


Import HouseInfo

To start, open the file called temperature_info.py in the sensor folder.

At the top of the file, import HouseInfo from the house_info module.
2
Create TemperatureData Class

Create a child class called TemperatureData that inherits the properties and methods from the HouseInfo class.

Still in the TemperatureData class, create a private method called _convert_data() with two parameters, self, and data. This method will help us convert the temperature data.

In the body of the _convert_data() method, create a variable called recs and set it to an empty list.
3
Convert Temperature Data

On a new line in the _convert_data() method, create a for loop to iterate over data. Use rec as your iterator variable.

In the body of the for, convert the rec string values to integers with base 10, and append them to recs.

    Note (more on the conversion process): The data parameter is a list of strings. These strings are integers, base 10, which are temperatures. You should use the int() constructor to convert these strings to integers passing base=10 as the second argument.

Finally, your method should return recs (outside of the for loop, and at the very end of the method).
4
Filter Temperature Data Records by Area

Next, we are going to override the get_data_by_area() method from the parent class.

Create a method called get_data_by_area() with two parameters, self and rec_area. The rec_area parameter should have a default value of 0, which translates to all records. The purpose of this method is to filter the temperature data by the "area" field. In this method rec_area maps to the "area" data column.

In the body of the get_data_by_area() method, create a variable called recs, and set it to the parent get_data_by_area() method. Call that parent method, and pass "temperature" as the first argument, and rec_area as the second argument. Hint: parent class methods can be access by using super.
5
Return Transformed Temperature Data Records by Area

Still in the get_data_by_area() method, return a call to the _convert_data() private method, passing recs as the only argument.
6
Filter Temperature Data Records by Date

Similarly, we are going to override get_data_by_date() method from the parent class.

Still in the TemperatureData class, create another method called get_data_by_date() with two parameters, self and rec_date. The rec_date parameter should have a default value set to the current date. You can accomplish this using the date module. The purpose of this method is to filter the temperature data by the "date" field. In this method, rec_date maps to the "date" data column.

    At the top of the file, import date from the datetime module. See date information and datetime information

In the body of the get_data_by_date() method, create a variable called recs and set it to the parent get_data_by_date() method. Pass "temperature" as the first argument, and rec_date as the second argument.
7
Return Transformed Temperature Data Records by Date

Still in the get_data_by_date() method, return a call to the _convert_data() private method, passing recs as the only argument.
8
Get Temperature Data by Area with sensor_app

Open the sensor_app.py file in the sensor directory. At the top of the file, from the temperature_info module, import the TemperatureData class.

At the bottom of the file, create an instance of the TemperatureData class, and assign it to a variable named temperature_data. Pass data as the argument to the TemperatureData() constructor.

Next, assign to recs and the result of calling get_data_by_area() from the temperature_data object. The get_data_by_area() method should take rec_area=test_area as the only argument.

Print the length of the recs list, also, print the maximum and minimum values in the recs list.

print("\nHouse Temperature sensor records for area {} = {}".format(test_area, len(recs)))
print("\tMaximum: {0}, Minimum: {1} temperatures".format(max(recs), min(recs)))

To preview your app, open a terminal at the root of the project and run the following command:

python sensor/sensor_app.py

Sample output does not includes previous tasks:

... # previous output

House Temperature sensor records for area 1 = 1000
        Maximum: 80, Minimum: 60 temperatures

FYI: the project's tests will not validate your print() statements.
9
Get Temperature Data by Date with sensor_app

Still in the sensor_app file, set the recs variable to the return value of get_data_by_date() method of the temperature_data object. The method takes rec_date=test_date as the only argument.

Print the test_date using strftime(), passing "%m/%d/%y" as the first argument, and the length of the recs list. Also print the maximum and minimum values in the recs list.

print("\nHouse Temperature sensor records for date: {} = {}".format(
    test_date.strftime("%m/%d/%y"), len(recs))
print("\tMaximum: {0}, Minimum: {1} temperatures".format(max(recs), min(recs)))

To preview your app, open a terminal at the root of the project and run the following command:

python sensor/sensor_app.py

Sample output does not includes previous tasks:

...

House Temperature sensor records for area 1 = 1000
        Maximum: 80, Minimum: 60 temperatures

House Temperature sensor records for date: 05/09/20 = 20
        Maximum: 82, Minimum: 80 temperatures

FYI: the project's tests will not validate your print() statements.

## Analyze Humidity and Air Quality Data

Create HumidityData Class

To start, open the file called humidity_info.py in the sensor folder.

At the top of the file, import HouseInfo from the house_info module.

Create a child class called HumidityData that inherits the properties and methods from the HouseInfo class.

Still in the HumidityData class, create a private method called _convert_data() with two parameters, self and data. This method will help us convert the humidity data.

In the body of the _convert_data() method, create a variable called recs and set it to an empty list.
2
Convert Humidity Data

On a new line in the _convert_data() method, create a for loop to iterate over data. Use rec as your iterator variable.

In the body of the for convert the rec string values to float and multiply it by 100, then, append them to recs.

    Note: The data parameter is a list of strings. These strings represent percentages of humidity in floating point numeric form. You should use the float() constructor to convert these numbers.

Finally, your method should return recs (outside of the for loop, and at the very end of the method).
3
Filter Humidity Data Records by Area

Next, you are going to override the get_data_by_area() method from the parent class.

Here, you are going to repeat the process you followed for the TemperatureClass. Create a method called get_data_by_area() with two parameters, self and rec_area. The rec_area parameter should have a default value of 0, which translates to all records. The purpose of this method is to filter the humidity data by the "area" field. In this method, rec_area maps to the "area" data column.

This method should be almost identical to the one you created for the TemperatureData class, with the exception of the field argument. This time, use "humidity" as the filter value.

The method should look like this:

def get_data_by_area(self, rec_area=0):
    recs = super().get_data_by_area("humidity", rec_area)
    return self._convert_data(recs)

4
Filter Humidity Data Records by Date

Similarly, you are going to override the get_data_by_date() method from the parent class.

At the top of the file, import date and datetime from the datetime module. See date information and datetime information

You are going to repeat the process you followed for the TemperatureClass. In the HumidityData class, create another method called get_data_by_date() with two parameters, self and rec_date. The rec_date parameter should have a default value set to today's date. You can accomplish this using the date module. The purpose of this method is to filter the humidity data by the "date" field. In this method, rec_date maps to the "date" data column.

This method should be almost identical to the one you created for the TemperatureData class, with the exception of the field argument. This time, use "humidity" as the filter value.

The method should look like this:

def get_data_by_date(self, rec_date=date.today()):
    recs = super().get_data_by_date("humidity", rec_date)
    return self._convert_data(recs)

5
Get Humidity Data by Area with sensor_app

Open the sensor_app.py file in the sensor directory. At the top of the file, from the humidity_info module, import HumidityData.

At the bottom of the file, create an instance of the HumidityData class, and assign it to a variable named humidity_data. Pass data as the argument to the HumidityData constructor.

Next, create a variable called recs and set it to the get_data_by_area() method of the humidity_data object. The get_data_by_area() method should take rec_area=test_area as the only argument.

Next, print the length of the recs list by area. Then, print the arithmetic mean of the recs values. To calculate the arithmetic mean, at the top of the file, from the statistics module, import mean.

print("\nHouse Humidity sensor records for area {} = {}".format(test_area, len(recs)))
print("\tAverage: {} humidity".format(mean(recs)))

To preview your app, open a terminal at the root of the project and run the following command:

python sensor/sensor_app.py

Sample output does not includes previous tasks:

... # previous output

House Humidity sensor records for area 1 = 1000
  Average: 60.19 humidity

FYI: this project's tests will not validate your print() statements.
6
Get Humidity Data by Date with sensor_app

Still in the sensor_app file, set the recs variable to the return value of the get_data_by_date() method of the humidity_data object. The method takes rec_date=test_date as the only argument.

Next, print the test_date using strftime(), passing "%m/%d/%y" as the first argument, and the length of the recs list as the second. Then, print the average of the recs records:

print("House Humidity sensor records for date: {} = {}".format( test_date.strftime("%m/%d/%y"), len(recs)))
print("\tAverrage: {} humidity".format(mean(recs)))

To preview your app, open a terminal at the root of the project and run the following command:

python sensor/sensor_app.py

Sample output does not includes previous tasks:

... # previous output

House Humidity sensor records for area 1 = 1000
        Average: 60.19 humidity
House Humidity sensor records for date: 05/09/20 = 20
        Averrage: 54.8 humidity

FYI: this project's tests will not validate your print() statements.
7
Create ParticleData Class

Now, it is time to work on the ParticleData class. To start, open the file called particle_count_info.py in the sensor folder.

At the top of the file, import HouseInfo from the house_info module.

Create a child class called ParticleData with HouseInfo as its parent.

Still in the ParticleData class, create a private method called _convert_data() with two parameters, self, and data. This method will help us convert the particle data.

In the body of the _convert_data() method, create a variable called recs and set it to an empty list.
8
Convert Particle Count Data

On a new line in the _convert_data() method, create a for loop to iterate over data. Use rec as your iterator variable.

In the body of the for, convert the rec string values to float, and append them to recs.

    Note: The data parameter is a list of strings. These strings represent particle concentrations in the air. The values are stored in scientific notation. To convert these values, use the float() constructor to convert these numbers.

Finally, your method should return recs (outside of the for loop, and at the very end of the method).
9
Filter Particle Count Data Records by Area and Date

Next, we are going to override the get_data_by_area() and get_data_by_date() methods from the parent class.

At the top of the file, import date and datetime from the datetime module.

This time, when you call the parent get_data_by_area() or get_data_by_date() methods, use "particulate" as the filter value.

The methods should look like this:

def get_data_by_area(self, rec_area=0):
    recs = super().get_data_by_area("particulate", rec_area)
    return self._convert_data(recs)

def get_data_by_date(self, rec_date=date.today()):
    recs = super().get_data_by_date("particulate", rec_date)
    return self._convert_data(recs)

10
Get Particle Count Concentrations

Next, add another method to the ParticleData class and called it get_data_concentrations(). The method should take two parameters, self and data. The purpose of this method is to take a list of particle data values, and group the data based on particle concentration on the air.

On a new line in the method, define a dictionary called particulate and initialize it to have three items. Their keys are "good", "moderate", and "bad", and all of them have a value of 0.
11
Return Particle Count Concentrations

Create a loop over the data list using rec as the iterator.

In the body of the for loop, update the particulate dictionary with the number of instances the rec value falls under the "good", "moderate", or "bad" category.

    When the particle concentration is 50.0 units or less, then it is considered "good".
    When the concentration is more than 50.0 and less than or equal to 100.0, it is considered "moderate".
    Anything above 100.0 is considered "bad".

Finally, your method should return particulate (outside of the for loop, and at the very end of the method)
12
Get Particle Data by Area with sensor_app

Open the sensor_app.py file in the sensor directory. At the top of the file, from the particle_count_info module, import ParticleData.

At the bottom of the file, create an instance of the ParticleData class, and assign it to a variable named particle_data. Pass the constructor data as the only argument.

Create a variable called recs and set it to the get_data_by_area() method of the particle_data object. The get_data_by_area() method should take rec_area=test_area as the only argument.

Next, print the length of the recs list by area.

print("\nHouse Particle sensor records for area {} = {}".format(test_area, len(recs))

Create a variable called concentrations and set it to the get_data_concentrations() method of the particle_data object, passing the data=recs as the only argument.

Next, print each of the concentrations.

print("\tGood Air Quality Recs: {}".format(concentrations["good"]))
print("\tModerate Air Quality Recs: {}".format(concentrations["moderate"]))
print("\tBad Air Quality Recs: {}".format(concentrations["bad"]))

To preview your app, open a terminal at the root of the project and run the following command:

python sensor/sensor_app.py

Sample output does not includes previous tasks:

... # previous output

House Particle sensor records for area 1 = 1000
      Good Air Quality Recs: 284
      Moderate Air Quality Recs: 366
      Bad Air Quality Recs: 350

FYI: the project's tests will not validate your print() statements.
13
Get Particle Data by Date with sensor_app

Still in the sensor_app file, set the recs variable to the return value of get_data_by_date() method of the particle_data object. The method takes rec_date=test_date as the only argument.

Next, print the test_date, using the strftime() passing it "%m/%d/%y", as the first argument, and the length of the recs list as the second argument:

print("\nHouse Particle sensor records for date: {} = {}".format( test_date.strftime("%m/%d/%y"), len(recs)))

Set concentrations and to the get_data_concentrations() method of the particle_data object, passing the data=recs as the only argument.

Next, print each of the concentrations by the test date.

print("\tGood Air Quality Recs: {}".format(concentrations["good"]))
print("\tModerate Air Quality Recs: {}".format(concentrations["moderate"]))
print("\tBad Air Quality Recs: {}".format(concentrations["bad"]))

To preview your app, open a terminal at the root of the project and run the following command:

python sensor/sensor_app.py

Sample output does not includes previous tasks:

... # previous output
House Particle sensor records for area 1 = 1000
        Good Air Quality Recs: 284
        Moderate Air Quality Recs: 366
        Bad Air Quality Recs: 350

House Particle sensor records for date: 05/09/20 = 20
        Good Air Quality Recs: 0
        Moderate Air Quality Recs: 0
        Bad Air Quality Recs: 20

FYI: this project's tests will not validate your print() statements.


##  Analyze Energy Consumption Data

1
Create EnergyData Class

To start, open the file called energy_info.py in the sensor folder.

At the top of the file, import HouseInfo from the house_info module.

Create a child class called EnergyData that inherits from HouseInfo.

Still in the EnergyData class, create two class constants to help us process the energy data.

The first constant is called ENERGY_PER_BULB and has the value of 0.2.

The second constant is called ENERGY_BITS and it is set to the hexadecimal number 0x0F0
2
Get Energy Data

Still in the EnergyData class, create a private method called _get_energy() with two parameters, self, and rec. This method will help us extract the energy data information from energy_usage data field.

    The rec parameter is a string. This string represents the energy_usage in hexadecimal notation form.

    The energy_usage field comes as a three-digit hexadecimal (hex) number (12 bits), for example "0xfef". However, only the middle hex number (bits: 4-7 with index notation) represents the energy usage. In order to extract these bits, we will use bitwise operations

To extract the energy information, three steps are required:

    Convert the rec string to an integer using int() constructor passing base=16 as the second argument, and assign the result to a new variable called energy. This will produce an integer to which you can apply bitwise operations.

    Isolate the energy bits by "anding" the energy integer with the ENERGY_BITS constant. This operation should clear all the bits from the first and third nibble. Assign the result back to energy.

    Then, right shift energy by four bits. Assign the result back to energy

Finally, return energy.
3
Convert Energy Data

Still in the EnergyData class, create a another private method called _convert_data() with two parameters, self and data. This method will help us convert the energy data.

In the body of the _convert_data() method, create a variable called recs, and set it to an empty list.

On a new line, create a for loop to iterate over data list. Use rec as your iterator variable.

    Note: The data parameter is a list of strings. These strings represent energy usage in hexadecimal form.

In the body of the for loop, convert the rec string values using the _get_energy() private method, then append them to recs.

Finally, your method should return recs (outside of the for loop, and at the very end of the method).
4
Filter Energy Usage Data Records by Area and Date

Next, we are going to override get_data_by_area() and get_data_by_date() methods from the parent class.

At the top of the file, import date and datetime from the datetime module.

Following the steps from the TemperatureData class, this time when you call the parent get_data_by_area() or get_data_by_date() methods, use "energy_usage" as the filter value.

The methods should look like this:

def get_data_by_area(self, rec_area=0):
    recs = super().get_data_by_area("energy_usage", rec_area)
    return self._convert_data(recs)

def get_data_by_date(self, rec_date=date.today()):
    recs = super().get_data_by_date("energy_usage", rec_date)
    return self._convert_data(recs)

5
Get Total Energy Usage

Next, add another method to the EnergyData class called calculate_energy_usage(). The method should take two parameters, self and data. The purpose of this method is to take a list of energy usage values, calculate the cost per light bulb usage, and return the sum of all the values in the data list.

On a new line in the method, define a variable called total_energy, which will store the sum of all converted values in the data list. To achieve this, call the sum built in function. This function should take a list comprehension as its only argument. The list comprehension should use field as the expression variable. The field variable should be multiplied by the ENERGY_PER_BULB constant.

Finally, return the total_energy.
6
Get Energy Data by Area with sensor_app

Open the sensor_app.py file in the sensor directory. At the top of the file, from the energy_info module, import EnergyData.

At the bottom of the file, create an instance of the EnergyData class, and assign it to a variable named energy_data. Pass data as the argument to the EnergyData constructor.

Assign to recs the result of calling get_data_by_area() of the energy_data object. The get_data_by_area() method should take rec_area=test_area as the only argument.

Next, print the length of the recs list by area.

print("\nHouse Energy sensor records for area {} = {}".format(test_area, len(recs)))

Create a variable called total_energy, and set it to the calculate_energy_usage() method of the energy_data object, passing it data=recs as the only argument.

Next, print the total energy usage:

print("\tEnergy Usage: {:2.2} Watts".format(total_energy))

To preview your app, open a terminal at the root of the project and run the following command:

python sensor/sensor_app.py

Sample output does not includes previous tasks:

... # previous output

House Energy sensor records for area 1 = 1000
        Energy Usage: 1.5e+03 Watts

FYI: this project's tests will not validate your print() statements.
7
Get Energy Data by Date with sensor_app

Still in the sensor_app file, set the recs variable to the return value of get_data_by_date() method of the energy_data object. The method takes rec_date=test_date as the only argument.

Next, print the test_date, using the strftime() passed "%m/%d/%y" as the first argument, and the length of the recs list as the second.

print("House Energy sensor records for date: {} = {}".format( test_date.strftime("%m/%d/%y"), len(recs)))

Set total_energy to the return value of calculate_energy_usage()from the energy_data object, passing data=recs as its only argument.

Next, print the total energy usage.

print("\tEnergy Usage: {:2.2} Watts".format(total_energy))

To preview your app, open a terminal at the root of the project and run the following command:

python sensor/sensor_app.py

Sample output does not includes previous tasks:

... # previous output
House Energy sensor records for area 1 = 1000
        Energy Usage: 1.5e+03 Watts
House Energy sensor records for date: 05/09/20 = 20
        Energy Usage: 1.9e+01 Watts

FYI: this project's tests will not validate your print() statements.
