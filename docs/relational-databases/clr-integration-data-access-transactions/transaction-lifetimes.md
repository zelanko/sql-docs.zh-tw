---
title: "交易存留期間 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- lifetimes [SQL Server]
- Transact-SQL vs. managed code
ms.assetid: cb076fda-6488-4959-a6a4-7adaccf3f25c
caps.latest.revision: "10"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 445984322c81766be4919cfda8b211a21e2519a0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="transaction-lifetimes"></a>交易存留期間
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]沒有一項重要差異交易間[!INCLUDE[tsql](../../includes/tsql-md.md)]在 managed 程式碼中啟動的預存的程序與： common language runtime (CLR) 程式碼不能利用交易狀態在進入或離開 CLR 引動過程。 請注意此差異的下列含意：  
  
-   在 CLR 框架內部啟動的交易必須認可或回復，否則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在離開框架時會產生錯誤。  
  
-   外部交易無法在 CLR 程式碼內部認可或回復。  
  
-   嘗試認可未在相同程序中啟動的交易時，會造成執行階段錯誤。  
  
-   嘗試回復未在相同程序中啟動的交易時，會造成交易停止回應 (以防發生其他任何副作用作業)。 交易會停止，直到 CLR 程式碼超出範圍為止。 請注意，當您在程序內部偵測到錯誤，而且想要確認整個交易結束時，這可能相當實用。  
  
## <a name="see-also"></a>請參閱＜  
 [CLR 整合和交易](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  
