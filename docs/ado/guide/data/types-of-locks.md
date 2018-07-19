---
title: 鎖定的類型 |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- AdLockBatchOptimistic [ADO]
- AdLockReadOnly [ADO]
- AdLockUnspecified [ADO]
- locks [ADO], types
- AdLockOptimistic [ADO]
- AdLockPessimistic [ADO]
ms.assetid: 12a978c0-b8a0-4ef0-87f0-a43c13659272
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 952030ca1edc6e13261021bb0e840adedf92535f
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35273137"
---
# <a name="types-of-locks"></a>鎖定的類型
## <a name="adlockbatchoptimistic"></a>adLockBatchOptimistic  
 表示開放式批次更新。 所需的批次更新模式。  
  
 許多應用程式會一次擷取的資料列數目，必須進行協調包括一整組要插入、 更新或刪除的資料列的更新。 與批次資料指標，只有一個需要往返伺服器，因此可改善更新效能並降低網路流量。 使用批次的資料指標程式庫，您就可以建立靜態資料指標，並再中斷與資料來源。 此時您可以進行變更的資料列和後續重新連接並將變更公佈到批次中的資料來源。  
  
## <a name="adlockoptimistic"></a>adLockOptimistic  
 指出提供者會使用開放式鎖定，鎖定資料錄，只有當您呼叫**更新**方法。 是另一位使用者可能會變更資料的時間之間可能發生這表示您編輯的記錄，當您呼叫**更新**，這樣就可以建立衝突。 在低衝突的機會的情況下使用這個鎖定類型，或可以輕易地解決衝突。  
  
## <a name="adlockpessimistic"></a>adLockPessimistic  
 指出封閉式鎖定、 記錄。 提供者沒有什麼是為了確保成功編輯資料錄，通常是在資料來源編輯之前立即鎖定記錄。 當然，這表示一旦您開始編輯，您釋出鎖定藉由呼叫前的記錄是其他使用者無法使用**更新。** 您不能有並行的變更資料，例如，保留系統中在系統中使用這種類型的鎖定。  
  
## <a name="adlockreadonly"></a>adLockReadOnly  
 表示唯讀的記錄。 您無法變更資料。 唯讀鎖定是鎖定的 「 快速 」 類型，因為它不需要伺服器維護記錄上的鎖定。  
  
## <a name="adlockunspecified"></a>adLockUnspecified  
 未指定鎖定的類型。
