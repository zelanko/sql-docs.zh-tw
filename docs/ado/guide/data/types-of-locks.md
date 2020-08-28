---
description: 鎖定的類型
title: 鎖定的類型 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- AdLockBatchOptimistic [ADO]
- AdLockReadOnly [ADO]
- AdLockUnspecified [ADO]
- locks [ADO], types
- AdLockOptimistic [ADO]
- AdLockPessimistic [ADO]
ms.assetid: 12a978c0-b8a0-4ef0-87f0-a43c13659272
author: rothja
ms.author: jroth
ms.openlocfilehash: 55087e96c0855f24153dee9bc279d9abf58d3f04
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979259"
---
# <a name="types-of-locks"></a>鎖定的類型
## <a name="adlockbatchoptimistic"></a>adLockBatchOptimistic  
 表示開放式批次更新。 批次更新模式的必要參數。  
  
 許多應用程式會一次提取多個資料列，然後需要進行協調更新，包括要插入、更新或刪除的整組資料列。 使用批次資料指標時，只需要對伺服器進行一次往返，進而改善效能並減少網路流量。 您可以使用批次資料指標程式庫，建立靜態資料指標，然後中斷與資料來源的連接。 至此，您可以對資料列進行變更，然後重新連接並將變更張貼到批次中的資料來源。  
  
## <a name="adlockoptimistic"></a>adLockOptimistic  
 指出提供者只有在您呼叫 **Update** 方法時，才會使用開放式鎖定鎖定記錄。 這表示當您編輯記錄時，可能會有另一位使用者變更資料，而當您呼叫 **Update**時，會產生衝突。 當衝突的機率很低或可以立即解決衝突的情況下，請使用此鎖定類型。  
  
## <a name="adlockpessimistic"></a>adLockPessimistic  
 指出封閉式鎖定、依記錄記錄。 提供者會執行必要的動作，以確保成功編輯記錄，通常是在編輯前立即鎖定資料來源的記錄。 當然，這表示在您開始編輯之後，其他使用者就無法使用記錄，除非您呼叫 Update 來釋放鎖定 **。** 在系統中使用這種類型的鎖定，您不能承受同時變更資料，例如保留系統中的資料。  
  
## <a name="adlockreadonly"></a>adLockReadOnly  
 表示唯讀記錄。 您無法變更資料。 唯讀鎖定是「最快」類型的鎖定，因為它不需要伺服器維護記錄的鎖定。  
  
## <a name="adlockunspecified"></a>adLockUnspecified  
 未指定鎖定的類型。
