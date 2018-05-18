---
title: AddMembers method of the MSFT\_SMReplicationGroup class
description: Adds members to the replication group.
audience: developer
author: REDMOND\\markl
manager: REDMOND\\markl
ms.assetid: '2092578e-3f3a-405b-85ad-3585397d4574'
ms.prod: 'windows-server-dev'
ms.technology: 'windows-management-instrumentation'
ms.tgt_platform: multiple
keywords: ["AddMembers method", "AddMembers method, MSFT_SMReplicationGroup class", "MSFT_SMReplicationGroup class, AddMembers method"]
topic_type:
- apiref
api_name:
- MSFT_SMReplicationGroup.AddMembers
api_location:
- StorageService.dll
api_type:
- COM
---

# AddMembers method of the MSFT\_SMReplicationGroup class

Adds members to the replication group.

## Syntax


```mof
UInt32 AddMembers(
  [in]������������MSFT_SMStorageObject REF StorageObjects[],
  [in, optional]��String ������������������username,
  [in, optional]��String ������������������password,
  [out]�����������MSFT_SMJob ����������REF Job,
  [out, optional]�MSFT_SMExtendedStatus ���ExtendedStatus
);
```



## Parameters

<dl> <dt>

*StorageObjects* \[in\]
</dt> <dd>

A reference to an array that contains the storage objects to add to the replication group.

</dd> <dt>

*username* \[in, optional\]
</dt> <dd>

The username used to authenticate the SMI-S provider.

</dd> <dt>

*password* \[in, optional\]
</dt> <dd>

The password used to authenticate the SMI-S provider.

</dd> <dt>

*Job* \[out\]
</dt> <dd>

If this operation is asynchronous, when this method returns, this parameter contains a reference to the object that represents the job; otherwise this parameter is set to **NULL**.

</dd> <dt>

*ExtendedStatus* \[out, optional\]
</dt> <dd>

When this method returns, this parameter contains a [**MSFT\_SMExtendedStatus**](msft-smextendedstatus.md) object that contains detailed status information about the results of this operation.

</dd> </dl>

## Return value

Returns "0" on success, otherwise returns a WMI error code.

## Requirements



|                                     |                                                                                               |
|-------------------------------------|-----------------------------------------------------------------------------------------------|
| Minimum supported client<br/> | None supported<br/>                                                                     |
| Minimum supported server<br/> | Windows Server�2016<br/>                                                                |
| Namespace<br/>                | Root\\Microsoft\\Windows\\Storage\\SM<br/>                                              |
| MOF<br/>                      | <dl> <dt>MsftStrgMan.mof</dt> </dl>    |
| DLL<br/>                      | <dl> <dt>StorageService.dll</dt> </dl> |



## See also

<dl> <dt>

[**MSFT\_SMReplicationGroup**](msft-smreplicationgroup.md)
</dt> </dl>

�

�




