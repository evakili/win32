﻿---
Description: 'Notifies the callback object that the status bar is being updated. Used by IShellFolderViewCB::MessageSFVCB.'
title: 'SFVM\_UPDATESTATUSBAR message'
---

# SFVM\_UPDATESTATUSBAR message

Notifies the callback object that the status bar is being updated. Used by [**IShellFolderViewCB::MessageSFVCB**](ishellfolderviewcb-messagesfvcb.md).


```C++
SFVM_UPDATESTATUSBAR 

    wParam = (WPARAM)(BOOL) fInitialize;

            
```



## Parameters

<dl> <dt>

*fInitialize* \[in\]
</dt> <dd>

A **BOOL** value that is set to **TRUE** if the status bar is being initialized.

</dd> </dl>

## Remarks

When you receive this notification:

-   Return S\_OK if you will handle the update.
-   Return MAKE\_HRESULT(SEVERITY\_SUCCESS,0,1) to have the system folder view object set the status bar text.
-   Return E\_FAIL to have the system folder view object handle the status bar.

The default status bar text is as follows.



| Status                      | Status bar text                         |
|-----------------------------|-----------------------------------------|
| No items selected           | "\#\# objects" (in the folder)          |
| One item selected           | The infotip for the item, if available. |
| More than one item selected | "\#\# objects selected"                 |



 

## Requirements



|                                     |                                                                                     |
|-------------------------------------|-------------------------------------------------------------------------------------|
| Minimum supported client<br/> | Windows 2000 Professional \[desktop apps only\]<br/>                          |
| Minimum supported server<br/> | Windows 2000 Server \[desktop apps only\]<br/>                                |
| Header<br/>                   | <dl> <dt>Shlobj.h</dt> </dl> |



 

 



