---
title: Support for device properties
author: windows-driver-content
description: Support for device properties
ms.assetid: ED9A67C4-DFD6-4CF1-B911-29570B3409A5
ms.author: windowsdriverdev
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Support for device properties


| Module                  | Class/Interface      |
|-------------------------|----------------------|
| AccelerometerDevice.cpp | CAccelerometerDevice |
| SensorDdi.cpp           | CSensorDdi           |
| SensorDevice.cpp        | CSensorDevice        |

 

The Windows sensor platform supports three categories of sensor properties:

Category
Description
General device properties
Includes a number of strings such as the device model, manufacturer name, and serial number. Also includes device-data like the current sensor state or the minimum report interval value. The properties in this category are read-only.
Per data-field properties
Properties that apply to the sensor’s data fields. For the accelerometer, these are the minimum, maximum, and resolution for each axis. The properties in this category are read only.
Settable device properties
Properties that an application can set. For the accelerometer, these are the change sensitivity and report interval.
 

The source file, SensorDdi.cpp, has three arrays of **PROPERTYKEY** structures that correspond to the three categories in the table above.

The first array has the general sensor properties - strings like the manufacturer's name, device model, and serial number. In addition, there are values like the minimum and maximum range, sensor resolution, and the minimum supported report interval.

```ManagedCPlusPlus
const PROPERTYKEY g_SupportedAccelerometerProperties[] =
{
    WPD_OBJECT_ID,
    SENSOR_PROPERTY_TYPE,
    SENSOR_PROPERTY_PERSISTENT_UNIQUE_ID,
    SENSOR_PROPERTY_MANUFACTURER, 
    SENSOR_PROPERTY_MODEL,
    SENSOR_PROPERTY_SERIAL_NUMBER,
    SENSOR_PROPERTY_FRIENDLY_NAME,
    SENSOR_PROPERTY_DESCRIPTION, 
    SENSOR_PROPERTY_CONNECTION_TYPE,
    SENSOR_PROPERTY_RANGE_MINIMUM,
    SENSOR_PROPERTY_RANGE_MAXIMUM,
    SENSOR_PROPERTY_RESOLUTION,
    SENSOR_PROPERTY_STATE,
    SENSOR_PROPERTY_MIN_REPORT_INTERVAL,
    WPD_FUNCTIONAL_OBJECT_CATEGORY,
};
```

The second array has three per data-field properties - the minimum and maximum range as well as the sensor resolution.

```ManagedCPlusPlus
const PROPERTYKEY g_SupportedPerDataFieldProperties[] =
{
    SENSOR_PROPERTY_RANGE_MINIMUM,
    SENSOR_PROPERTY_RANGE_MAXIMUM,
    SENSOR_PROPERTY_RESOLUTION,
};
```

The third array contains the accelerometer's change sensitivity and the current report interval.

```ManagedCPlusPlus
const PROPERTYKEY g_SettableAccelerometerProperties[] =
{
    SENSOR_PROPERTY_CHANGE_SENSITIVITY,
    SENSOR_PROPERTY_CURRENT_REPORT_INTERVAL,
};
```

### Setting the general and per data-field properties

The sample driver sets the general and per data-field properties during the initialization phase. The code that handles this work is found in the **CAccelerometerDevice::SetDefaultProperties** method. For information about the sequence of calls that set these properties, see [Driver initialization](driver-initialization.md).

### Setting the writeable properties

When a desktop, or WinRT, app sets the current report-interval, or, the change-sensitivity properties, the Sensors Class extension uses this sequence of methods to make the update.

| Method                                    | Calling object or method         | Description                                                                          |
|-------------------------------------------|----------------------------------|--------------------------------------------------------------------------------------|
| **CSensorDdi::OnSetProperties**           | SensorsClassExtension.dll        | The class extension invokes this method to start the property update.                |
| **CSensorDevice::SetProperties**          | **CSensorDdi::OnSetProperties**  | Applies the new property using the property-key and value supplied by the app.       |
| **CSensorDevice::ApplyUpdatedProperties** | **CSensorDevice::SetProperties** | Reapplies the new value since it may have altered the minimums stored by the driver. |

 

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bsensors\sensors%5D:%20Support%20for%20device%20%20properties%20%20RELEASE:%20%281/12/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


