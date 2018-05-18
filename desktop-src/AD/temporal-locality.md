---
title: Temporal Locality
description: Temporal locality is an avoidance strategy that reduces the window for partial updates.
audience: developer
author: REDMOND\\markl
manager: REDMOND\\mbaldwin
ms.assetid: '8f454087-46cb-4fa6-b83a-65b2393029c3'
ms.prod: 'windows-server-dev'
ms.technology: 'active-directory-domain-services'
ms.tgt_platform: multiple
---

# Temporal Locality

*Temporal locality* is an avoidance strategy that reduces the window for partial updates. Replication of changes from a given source replica proceeds in ascending USN order. Writes that occur close together in time will have USNs that are "near" each other, and will be propagated close together in time. Applications that create or update multiple, related objects should write the objects as close together in time as possible. For example, the application could gather all necessary input from the user and apply it to the directory when the user clicks an "Apply" button.

Temporal locality also reduces the odds of collision resolution introducing intra-object inconsistencies.

 

 



