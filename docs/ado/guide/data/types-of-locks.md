---
title: 鎖定的類型 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 93436a5180f1a01269f1612f7e608b71b4c073e9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67923803"
---
# <a name="types-of-locks"></a>鎖定的類型
## <a name="adlockbatchoptimistic"></a>adLockBatchOptimistic  
 表示開放式批次更新。 批次更新模式的必要參數。  
  
 許多應用程式會一次提取多個資料列，然後需要進行協調更新，包括要插入、更新或刪除的整組資料列。 使用批次資料指標時，只需要對伺服器進行一次往返，因此可改善更新效能並減少網路流量。 使用批次資料指標程式庫，您可以建立靜態資料指標，然後中斷與資料來源的連線。 此時，您可以對資料列進行變更，然後重新連接，並將變更張貼至批次中的資料來源。  
  
## <a name="adlockoptimistic"></a>adLockOptimistic  
 指出提供者只有在您呼叫**Update**方法時，才會使用開放式鎖定鎖定記錄。 這表示在您編輯記錄和呼叫**Update**時，另一位使用者可能會變更資料，這會產生衝突。 當發生衝突的機率很低，或可以隨時解決衝突的情況下，請使用此鎖定類型。  
  
## <a name="adlockpessimistic"></a>adLockPessimistic  
 表示封閉式鎖定，依記錄記錄。 提供者會執行必要的動作，以確保成功編輯記錄，通常是在編輯之前立即鎖定資料來源的記錄。 當然，這表示在您開始編輯之前，其他使用者無法使用記錄，直到您藉由呼叫 Update 來釋放鎖定為止 **。** 在系統中使用此類型的鎖定，而您無法承受對資料的並行變更，例如保留系統中的。  
  
## <a name="adlockreadonly"></a>adLockReadOnly  
 表示唯讀記錄。 您不能改變數據。 唯讀鎖定是「最快」的鎖定類型，因為它不需要伺服器維護記錄的鎖定。  
  
## <a name="adlockunspecified"></a>adLockUnspecified  
 未指定鎖定的類型。
