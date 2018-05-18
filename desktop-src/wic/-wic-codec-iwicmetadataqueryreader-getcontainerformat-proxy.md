---
Description: 'Proxy function for the GetContainerFormat method.'
ms.assetid: '3a909151-53c2-4f82-9ead-f689b73f5faf'
title: 'IWICMetadataQueryReader\_GetContainerFormat\_Proxy function'
---

# IWICMetadataQueryReader\_GetContainerFormat\_Proxy function

Proxy function for the [**GetContainerFormat**](-wic-codec-iwicmetadataqueryreader-getcontainerformat.md) method.

## Syntax


```C++
HRESULT IWICMetadataQueryReader_GetContainerFormat_Proxy(
  _In_��IWICMetadataQueryReader *THIS_PTR,
  _Out_�GUID �������������������*pguidContainerFormat
);
```



## Parameters

<dl> <dt>

*THIS\_PTR* \[in\]
</dt> <dd>

Type: **[**IWICMetadataQueryReader**](-wic-codec-iwicmetadataqueryreader.md)\***

Pointer to this [**IWICMetadataQueryReader**](-wic-codec-iwicmetadataqueryreader.md) object.

</dd> <dt>

*pguidContainerFormat* \[out\]
</dt> <dd>

Type: **GUID\***

Pointer that receives the cointainer format GUID.

</dd> </dl>

## Return value

Type: **HRESULT**

If this function succeeds, it returns **S\_OK**. Otherwise, it returns an **HRESULT** error code.

## Remarks

## Requirements



|                                     |                                                                                                                                                                  |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Minimum supported client<br/> | Windows�XP with SP2, Windows�Vista \[desktop apps only\]<br/>                                                                                              |
| Minimum supported server<br/> | Windows Server�2008 \[desktop apps only\]<br/>                                                                                                             |
| DLL<br/>                      | <dl> <dt>Windowscodecs.dll; </dt> <dt>Wincodec.lib</dt> </dl> |



�

�



