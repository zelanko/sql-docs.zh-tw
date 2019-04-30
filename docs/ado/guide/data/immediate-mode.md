---
title: 即時模式 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ADO], immediate mode
- immediate mode [ADO]
- updating data [ADO], immediate mode
ms.assetid: 31fc53d0-97de-4315-a87b-3bf5cdd1f432
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2ff8782287f5a6cbeb3f22ca58eaa3bd061c6c89
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63161507"
---
# <a name="immediate-mode"></a>即時模式
即時模式處於作用中時**LockType**屬性設定為**adLockOptimistic**或是**Locktype**。 在即時模式、 一筆記錄的變更會傳播至資料來源為您宣告工作的資料列完成藉由呼叫**更新**方法。  
  
## <a name="calling-update"></a>呼叫更新  
 如果您將記錄從您要加入或編輯，然後再呼叫**更新**方法，ADO 會自動會呼叫**更新**以儲存變更。 您必須呼叫**CancelUpdate**方法，再瀏覽，如果您想要取消目前的記錄所做的變更或捨棄新加入的記錄。  
  
 目前的記錄會保留目前之後呼叫**更新**方法。  
  
## <a name="cancelupdate"></a>CancelUpdate  
 使用**CancelUpdate**方法取消目前的資料列所做的變更，或捨棄新加入的資料列。 您無法取消目前的資料列或新的資料列的變更之後您呼叫,**更新**方法，除非所做的變更可以復原與交易的一部分**RollbackTrans**方法或部分批次更新。 您可以在批次更新的情況下，取消**更新**具有**CancelUpdate**或是**CancelBatch**方法。  
  
 如果您要新增新的資料列，當您呼叫**CancelUpdate**方法，目前的資料列會成為之前為目前的資料列**AddNew**呼叫。  
  
 如果您不變更目前的資料列或加入新的資料列，則呼叫**CancelUpdate**方法會產生錯誤。
