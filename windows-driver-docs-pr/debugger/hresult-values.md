---
title: HRESULT Values
description: The following is a list of common return values for functions and methods, and their usual meanings.
ms.assetid: 713f3ee2-2f5b-415e-9908-90f5ae428b43
ms.author: domars
ms.date: 12/07/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
keywords: ["HRESULT Values Windows Debugging"]
topic_type:
- apiref
api_name:
- HRESULT Values
api_location:
- DbgEng.h
api_type:
- HeaderDef
ms.date: 10/30/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# HRESULT Values


The following is a list of common return values for functions and methods, and their usual meanings.

## <span id="ddk_return_values_dbx"></span><span id="DDK_RETURN_VALUES_DBX"></span>


**Successful results.** These values are defined in WinError.h.

<span id="S_OK"></span><span id="s_ok"></span>S\_OK  
Successful completion.

<span id="S_FALSE"></span><span id="s_false"></span>S\_FALSE  
Completed without error, but only partial results were obtained.

If a buffer is not large enough to hold the information that is returned to it, the returned information is often truncated to fit into the buffer and S\_FALSE is returned from the method.

**Error results.** These values are defined in WinError.h.

<span id="E_FAIL"></span><span id="e_fail"></span>E\_FAIL  
The operation could not be performed.

<span id="E_INVALIDARG"></span><span id="e_invalidarg"></span>E\_INVALIDARG  
One of the arguments passed in was invalid.

<span id="E_NOINTERFACE"></span><span id="e_nointerface"></span>E\_NOINTERFACE  
The object searched for was not found.

<span id="E_OUTOFMEMORY"></span><span id="e_outofmemory"></span>E\_OUTOFMEMORY  
A memory allocation attempt failed.

<span id="E_UNEXPECTED"></span><span id="e_unexpected"></span>E\_UNEXPECTED  
The target was not accessible, or the engine was not in a state where the function or method could be processed.

<span id="E_NOTIMPL"></span><span id="e_notimpl"></span>E\_NOTIMPL  
Not implemented.

<span id="HRESULT_FROM_WIN32_ERROR_ACCESS_DENIED_"></span><span id="hresult_from_win32_error_access_denied_"></span>HRESULT\_FROM\_WIN32(ERROR\_ACCESS\_DENIED)  
The operation was denied because the debugger is in [Secure Mode](https://msdn.microsoft.com/library/windows/hardware/ff554760).

**NT error results.** Other error codes, such as STATUS\_CONTROL\_C\_EXIT and STATUS\_NO\_MORE\_ENTRIES, can sometimes occur. These results are passed to the HRESULT\_FROM\_NT macro that is defined in WinError.h before being returned.

**Win32 error results.** Other error codes, such as ERROR\_READ\_FAULT and ERROR\_WRITE\_FAULT, can sometimes occur. These results are passed to the HRESULT\_FROM\_WIN32 macro that is defined in WinError.h before being returned.

Requirements
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">DbgEng.h (include DbgEng.h)</td>
</tr>
</tbody>
</table>

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[debugger\debugger]:%20HRESULT%20Values%20%20RELEASE:%20%2811/30/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")



