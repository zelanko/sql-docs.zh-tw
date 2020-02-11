---
title: 立即模式 |Microsoft Docs
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
ms.openlocfilehash: 3952ef502bf79d6704cbaea80b9a825a3c70981b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67925018"
---
# <a name="immediate-mode"></a>即時模式
當**LockType**屬性設定為**adLockOptimistic**或**adLockPessimistic**時，立即模式就會生效。 在 [即時] 模式中，對記錄所做的變更會在您藉由呼叫**Update**方法，在資料列上宣告工作完成後，立即傳播至資料來源。  
  
## <a name="calling-update"></a>呼叫更新  
 如果您在呼叫**update**方法之前，從您要新增或編輯的記錄中移動，ADO 會自動呼叫**update**來儲存變更。 如果您想要取消對目前記錄所做的任何變更，或捨棄新加入的記錄，則必須在導覽前呼叫**CancelUpdate**方法。  
  
 呼叫**Update**方法之後，目前的記錄仍維持最新。  
  
## <a name="cancelupdate"></a>CancelUpdate  
 使用**CancelUpdate**方法可取消對目前資料列所做的任何變更，或捨棄新加入的資料列。 您無法在呼叫**Update**方法之後取消對目前資料列或新資料列所做的變更，除非變更是交易的一部分，而您可以使用**RollbackTrans**方法或批次更新的一部分來復原。 在批次更新的情況下，您可以使用**CancelUpdate**或**CancelBatch**方法來取消**更新**。  
  
 當您呼叫**CancelUpdate**方法時，如果要加入新的資料列，目前的資料列會成為**AddNew**呼叫之前的目前資料列。  
  
 如果您未變更目前的資料列或加入新的資料列，則呼叫**CancelUpdate**方法會產生錯誤。
