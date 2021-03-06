---
title: DispatchSetInformation Routines
author: windows-driver-content
description: DispatchSetInformation Routines
ms.assetid: 9fb56504-32a7-47b0-b731-df1dc74ce861
keywords: ["dispatch routines WDK kernel , DispatchSetInformation routine", "DispatchSetInformation routine", "set information dispatch routines WDK kernel", "IRP_MJ_SET_INFORMATION I/O function code"]
ms.author: windowsdriverdev
ms.date: 06/16/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# DispatchSetInformation Routines


## <a href="" id="ddk-dispatchsetinformation-routines-kg"></a>


A driver's [*DispatchSetInformation*](https://msdn.microsoft.com/library/windows/hardware/ff543399) routine handles IRPs for the [**IRP\_MJ\_SET\_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/ff550799) I/O function code. Driver support for this I/O function code is optional, and typically appears in higher-level or file system drivers. This request is sent by the I/O manager and other operating system components, as well as other kernel-mode drivers. For example, it is sent when a user-mode application calls [**SetEndOfFile**](https://msdn.microsoft.com/library/windows/desktop/aa365531), and when a kernel-mode component calls [**ZwSetInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567096).

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bkernel\kernel%5D:%20DispatchSetInformation%20Routines%20%20RELEASE:%20%286/14/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


