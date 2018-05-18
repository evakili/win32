---
Description: 'To enumerate the battery devices on a local computer, use the SetupDiGetClassDevs function.'
ms.assetid: '17e3c779-91ba-4901-9435-b73dedbf0b89'
title: Enumerating Battery Devices
---

# Enumerating Battery Devices

To enumerate the battery devices on a local computer, use the [SetupDiGetClassDevs](http://go.microsoft.com/fwlink/p/?linkid=91493) function. The *ClassGuid* parameter is a pointer to **GUID\_DEVCLASS\_BATTERY** (defined in BatClass.h). To enumerate all of the batteries, set the *Enumerator* parameter to **NULL** and set the *Flags* parameter to **DIGCF\_PRESENT** \| **DIGCF\_INTERFACEDEVICE**. To obtain the names of the battery devices, use the [SetupDiEnumDeviceInterfaces](http://go.microsoft.com/fwlink/p/?linkid=91492) and [SetupDiGetDeviceInterfaceDetail](http://go.microsoft.com/fwlink/p/?linkid=91494) functions on the data returned. To open a file handle for each of the battery devices, call the [**CreateFile**](https://msdn.microsoft.com/library/windows/desktop/aa363858) function with these names.

The following C++ example shows how to enumerate battery devices on a local computer.


```C++
DWORD GetBatteryState()
 {
#define GBS_HASBATTERY 0x1
#define GBS_ONBATTERY  0x2
  // Returned value includes GBS_HASBATTERY if the system has a 
  // non-UPS battery, and GBS_ONBATTERY if the system is running on 
  // a battery.
  //
  // dwResult & GBS_ONBATTERY means we have not yet found AC power.
  // dwResult & GBS_HASBATTERY means we have found a non-UPS battery.

  DWORD dwResult = GBS_ONBATTERY;

  // IOCTL_BATTERY_QUERY_INFORMATION,
  // enumerate the batteries and ask each one for information.

  HDEVINFO hdev =
            SetupDiGetClassDevs(&amp;GUID_DEVCLASS_BATTERY, 
                                0, 
                                0, 
                                DIGCF_PRESENT | DIGCF_DEVICEINTERFACE);
  if (INVALID_HANDLE_VALUE != hdev)
   {
    // Limit search to 100 batteries max
    for (int idev = 0; idev < 100; idev++)
     {
      SP_DEVICE_INTERFACE_DATA did = {0};
      did.cbSize = sizeof(did);

      if (SetupDiEnumDeviceInterfaces(hdev,
                                      0,
                                      &amp;GUID_DEVCLASS_BATTERY,
                                      idev,
                                      &amp;did))
       {
        DWORD cbRequired = 0;

        SetupDiGetDeviceInterfaceDetail(hdev,
                                        &amp;did,
                                        0,
                                        0,
                                        &amp;cbRequired,
                                        0);
        if (ERROR_INSUFFICIENT_BUFFER == GetLastError())
         {
          PSP_DEVICE_INTERFACE_DETAIL_DATA pdidd =
            (PSP_DEVICE_INTERFACE_DETAIL_DATA)LocalAlloc(LPTR,
                                                         cbRequired);
          if (pdidd)
           {
            pdidd->cbSize = sizeof(*pdidd);
            if (SetupDiGetDeviceInterfaceDetail(hdev,
                                                &amp;did,
                                                pdidd,
                                                cbRequired,
                                                &amp;cbRequired,
                                                0))
             {
              // Enumerated a battery.  Ask it for information.
              HANDLE hBattery = 
                      CreateFile(pdidd->DevicePath,
                                 GENERIC_READ | GENERIC_WRITE,
                                 FILE_SHARE_READ | FILE_SHARE_WRITE,
                                 NULL,
                                 OPEN_EXISTING,
                                 FILE_ATTRIBUTE_NORMAL,
                                 NULL);
              if (INVALID_HANDLE_VALUE != hBattery)
               {
                // Ask the battery for its tag.
                BATTERY_QUERY_INFORMATION bqi = {0};

                DWORD dwWait = 0;
                DWORD dwOut;

                if (DeviceIoControl(hBattery,
                                    IOCTL_BATTERY_QUERY_TAG,
                                    &amp;dwWait,
                                    sizeof(dwWait),
                                    &amp;bqi.BatteryTag,
                                    sizeof(bqi.BatteryTag),
                                    &amp;dwOut,
                                    NULL)
                    &amp;&amp; bqi.BatteryTag)
                 {
                  // With the tag, you can query the battery info.
                  BATTERY_INFORMATION bi = {0};
                  bqi.InformationLevel = BatteryInformation;

                  if (DeviceIoControl(hBattery,
                                      IOCTL_BATTERY_QUERY_INFORMATION,
                                      &amp;bqi,
                                      sizeof(bqi),
                                      &amp;bi,
                                      sizeof(bi),
                                      &amp;dwOut,
                                      NULL))
                   {
                    // Only non-UPS system batteries count
                    if (bi.Capabilities & BATTERY_SYSTEM_BATTERY)
                     {
                      if (!(bi.Capabilities & BATTERY_IS_SHORT_TERM))
                       {
                        dwResult |= GBS_HASBATTERY;
                       }

                      // Query the battery status.
                      BATTERY_WAIT_STATUS bws = {0};
                      bws.BatteryTag = bqi.BatteryTag;

                      BATTERY_STATUS bs;
                      if (DeviceIoControl(hBattery,
                                          IOCTL_BATTERY_QUERY_STATUS,
                                          &amp;bws,
                                          sizeof(bws),
                                          &amp;bs,
                                          sizeof(bs),
                                          &amp;dwOut,
                                          NULL))
                       {
                        if (bs.PowerState & BATTERY_POWER_ON_LINE)
                         {
                          dwResult &amp;= ~GBS_ONBATTERY;
                         }
                       }
                     }
                   }
                 }
                CloseHandle(hBattery);
               }
             }
            LocalFree(pdidd);
           }
         }
       }
        else  if (ERROR_NO_MORE_ITEMS == GetLastError())
         {
          break;  // Enumeration failed - perhaps we're out of items
         }
     }
    SetupDiDestroyDeviceInfoList(hdev);
   }

  //  Final cleanup:  If we didn't find a battery, then presume that we
  //  are on AC power.

  if (!(dwResult & GBS_HASBATTERY))
    dwResult &amp;= ~GBS_ONBATTERY;

  return dwResult;
 }
```



To enumerate the battery devices connected to a remote computer, use the [**Win32\_Battery**](https://msdn.microsoft.com/library/aa394074) WMI class in a client script or application.

## Related topics

<dl> <dt>

[SetupDiGetClassDevs](http://go.microsoft.com/fwlink/p/?linkid=91493)
</dt> <dt>

[SetupDiEnumDeviceInterfaces](http://go.microsoft.com/fwlink/p/?linkid=91492)
</dt> <dt>

[SetupDiGetDeviceInterfaceDetail](http://go.microsoft.com/fwlink/p/?linkid=91494)
</dt> <dt>

[**IOCTL\_BATTERY\_QUERY\_TAG**](ioctl-battery-query-tag.md)
</dt> <dt>

[**IOCTL\_BATTERY\_QUERY\_INFORMATION**](ioctl-battery-query-information.md)
</dt> <dt>

[**IOCTL\_BATTERY\_QUERY\_STATUS**](ioctl-battery-query-status.md)
</dt> </dl>

 

 


