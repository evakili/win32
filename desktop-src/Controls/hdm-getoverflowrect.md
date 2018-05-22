---
title: HDM\_GETOVERFLOWRECT message
description: Gets the bounding rectangle of the overflow button when the HDS\_OVERFLOW style is set on the header control and the overflow button is visible. Send this message explicitly or by using the Header\_GetOverflowRect macro.
ms.assetid: '52fb3dc3-ce22-40da-8222-20fd75c005ae'
keywords: ["HDM_GETOVERFLOWRECT message Windows Controls"]
topic_type:
- apiref
api_name:
- HDM_GETOVERFLOWRECT
api_location:
- Commctrl.h
api_type:
- HeaderDef
---

# HDM\_GETOVERFLOWRECT message

Gets the bounding rectangle of the overflow button when the [**HDS\_OVERFLOW**](header-control-styles.md#hds-overflow) style is set on the header control and the overflow button is visible. Send this message explicitly or by using the [**Header\_GetOverflowRect**](header-getoverflowrect.md) macro.

## Parameters

<dl> <dt>

*wParam* 
</dt> <dd>

Not used. Must be zero.

</dd> <dt>

*lParam* \[in\]
</dt> <dd>

A pointer to a [**RECT**](https://msdn.microsoft.com/library/windows/desktop/dd162897) structure to receive the bounding rectangle information. The message sender is responsible for allocating this structure. The coordinates returned in the **RECT** structure are expressed as screen coordinates.

</dd> </dl>

## Return value

Returns **TRUE** if successful; otherwise, **FALSE**.

## Remarks

The header control must have style **HDF\_SPLITBUTTON**.

## Requirements



|                                     |                                                                                       |
|-------------------------------------|---------------------------------------------------------------------------------------|
| Minimum supported client<br/> | Windows�Vista \[desktop apps only\]<br/>                                        |
| Minimum supported server<br/> | Windows Server�2008 \[desktop apps only\]<br/>                                  |
| Header<br/>                   | <dl> <dt>Commctrl.h</dt> </dl> |



## See also

<dl> <dt>

[About Header Controls](header-controls.md)
</dt> </dl>

�

�




