---
title: Querying for the Display of a Custom UI
description: Querying for the Display of a Custom UI
ms.assetid: 89f39281-db97-4cbe-8753-43ab30d840c8
keywords: ["custom UI WDK Native 802.11 IHV UI Extensions DLL , querying", "querying custom UI display"]
---

# Querying for the Display of a Custom UI


**Important**  The [Native 802.11 Wireless LAN](native-802-11-wireless-lan4.md) interface is deprecated in Windows 10 and later. Please use the WLAN Device Driver Interface (WDI) instead. For more information about WDI, see [WLAN Universal Windows driver model](wifi-universal-driver-model.md).

 

The operating system can query the Native 802.11 IHV Extensions DLL to determine whether the DLL has a custom UI to display. The operating system queries the DLL whenever the wireless LAN (WLAN) adapter transitions to one of the following phases within the WLAN network connection process.

<a href="" id="pre-association-------"></a>**Pre-association**   
The connection phase before the IHV Extensions DLL initiates a pre-association operation. For more information about the pre-association operation, see [Pre-Association Operations](pre-association-operations.md).

<a href="" id="post-association-------"></a>**Post-association**   
The connection phase after the IHV Extensions DLL completes a post-association operation. For more information about the post-association operation, see [Post-Association Operations](post-association-operations.md).

The operating system calls the Native 802.11 IHV Extensions DLL's [*Dot11ExtIhvQueryUIRequest*](https://msdn.microsoft.com/library/windows/hardware/ff547507) IHV Handler function to query whether a custom UI can be displayed. The operating system passes the current phase of the connection process through the *connectionPhase* parameter. If a custom UI must be displayed, the DLL returns a [**DOT11EXT\_IHV\_UI\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff547637) structure through the p *pIhvUIRequest* parameter.

Through the [**DOT11EXT\_IHV\_UI\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff547637) structure, the Native 802.11 IHV Extensions DLL specifies the custom UI through the following data.

-   The user session identifier (ID), which is used to identify a specific user context.

-   A globally unique ID (GUID), which identifies the specific UI request.

-   The class ID (CLSID) of **IWizardExtension** COM interface that is implemented within the Native 802.11 IHV UI Extensions DLL. The CLSID is used to request a specific custom UI that is supported by the DLL.

    For more information about the **IWizardExtension** COM interface, see [IWizardExtension COM Interface](http://go.microsoft.com/fwlink/p/?linkid=56607).

-   A buffer that contains data in a proprietary format that is defined by the independent hardware vendor (IHV) and processed by the specified **IWizardExtension** COM interface. For example, the buffer could contain the default values that are displayed within the custom UI.

The custom UI will be displayed as a set of wizard pages within the standard Network Connection UI. For more information about this process, see [Displaying Custom UI Pages within the Network Connection Wizard](displaying-custom-ui-pages-within-the-network-connection-wizard.md).

 

 





