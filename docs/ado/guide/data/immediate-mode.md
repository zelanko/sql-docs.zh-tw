---
title: "即時模式 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data updates [ADO], immediate mode
- immediate mode [ADO]
- updating data [ADO], immediate mode
ms.assetid: 31fc53d0-97de-4315-a87b-3bf5cdd1f432
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 714cbcae65121a92f8a38bbcf93fbb472ada5573
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="immediate-mode"></a>即時模式
即時模式就是作用中時**LockType**屬性設定為**Adlockreadonly**或**Locktype**。 在即時模式中，記錄的變更會傳播到資料來源為您宣告工作的資料列上完成藉由呼叫**更新**方法。  
  
## <a name="calling-update"></a>呼叫更新  
 如果您將記錄從您要加入或編輯，然後再呼叫**更新**自動呼叫方法時，ADO 會**更新**儲存的變更。 您必須呼叫**CancelUpdate**方法，再瀏覽，如果您想要取消目前的記錄所做的變更或捨棄新加入的記錄。  
  
 目前的記錄會保留目前之後呼叫**更新**方法。  
  
## <a name="cancelupdate"></a>CancelUpdate  
 使用**CancelUpdate**方法來取消目前的資料列所做的變更或捨棄新加入的資料列。 您無法取消目前的資料列或新的資料列的變更之後您呼叫,**更新**方法，除非所做的變更可以回復與交易的一部分，否則**RollbackTrans**方法或部分批次更新。 在批次更新，您可以取消**更新**與**CancelUpdate**或**CancelBatch**方法。  
  
 如果您要加入新的資料列，當您呼叫**CancelUpdate**方法中，目前的資料列變成資料列之前的目前**AddNew**呼叫。  
  
 如果您有不變更目前的資料列，或加入新的資料列，則呼叫**CancelUpdate**方法會產生錯誤。
