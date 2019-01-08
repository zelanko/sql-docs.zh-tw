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
manager: craigg
ms.openlocfilehash: 6b66b87b0c741bf943cc2558862a0e1853c386b5
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52510728"
---
# <a name="types-of-locks"></a>鎖定的類型
## <a name="adlockbatchoptimistic"></a>adLockBatchOptimistic  
 表示開放式的批次更新。 批次更新模式的必要項。  
  
 許多應用程式一次擷取的資料列數目，然後必須進行協調包括一整組的插入、 更新或刪除的資料列的更新。 與批次資料指標，只有一個需要往返伺服器，進而改善更新效能並降低網路流量。 您可以使用批次的資料指標程式庫，來建立靜態資料指標，然後中斷連接資料來源的項目。 此時您可以變更資料列和之後重新連線，而且將變更公佈到批次中的資料來源。  
  
## <a name="adlockoptimistic"></a>adLockOptimistic  
 指出提供者會使用開放式鎖定-只有當您呼叫時鎖定資料錄**更新**方法。 這表示會有另一位使用者可能會變更的時間之間的資料有機會您編輯的記錄和當您呼叫**更新**，這會建立衝突。 在其中的衝突很低的情況下使用此鎖定類型，或可以輕易地解決衝突。  
  
## <a name="adlockpessimistic"></a>adLockPessimistic  
 表示封閉式鎖定，記錄。 提供者會執行什麼是為了確保成功編輯記錄，通常是透過在資料來源編輯之前，立即鎖定記錄。 當然，這表示一旦您開始編輯時，您藉由呼叫釋放鎖定之前的記錄是其他使用者無法使用**更新。** 您不得將並行的變更資料，例如，在保留系統在系統中使用這種類型的鎖定。  
  
## <a name="adlockreadonly"></a>adLockReadOnly  
 表示唯讀的記錄。 您無法改變的資料。 唯讀鎖定會是鎖定的 「 最快速 」 類型，因為它不需要伺服器維護記錄的鎖定。  
  
## <a name="adlockunspecified"></a>adLockUnspecified  
 未指定鎖定的類型。
