---
title: 立即模式 |Microsoft Docs
description: 描述立即模式，它會在 LockType 屬性設定為 adLockOptimistic 或 adLockPessimistic 時生效。
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ADO], immediate mode
- immediate mode [ADO]
- updating data [ADO], immediate mode
ms.assetid: 31fc53d0-97de-4315-a87b-3bf5cdd1f432
author: rothja
ms.author: jroth
ms.openlocfilehash: e57d39fedb6509663ec21f28341d6bbca57dbd5c
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980499"
---
# <a name="immediate-mode"></a>即時模式
當 **LockType** 屬性設定為 **adLockOptimistic** 或 **adLockPessimistic**時，立即模式會生效。 在「立即模式」中，當您藉由呼叫 **Update** 方法在資料列完成宣告工作時，會立即將記錄的變更傳播至資料來源。  
  
## <a name="calling-update"></a>呼叫更新  
 如果您在呼叫 **update** 方法之前從要新增或編輯的記錄中移動，ADO 會自動呼叫 **update** 來儲存變更。 如果您想要取消對目前記錄所做的任何變更，或是捨棄新加入的記錄，則必須在導覽之前呼叫 **CancelUpdate** 方法。  
  
 當您呼叫 **Update** 方法之後，目前的記錄仍保持為最新狀態。  
  
## <a name="cancelupdate"></a>CancelUpdate  
 您可以使用 **CancelUpdate** 方法來取消對目前資料列所做的任何變更，或是捨棄新加入的資料列。 您無法在呼叫 **Update** 方法之後取消目前資料列或新資料列的變更，除非變更是交易的一部分，您可以使用 **RollbackTrans** 方法或批次更新的一部分來復原這些變更。 在批次更新的案例中，您可以使用**CancelUpdate**或**CancelBatch**方法來取消**更新**。  
  
 如果您在呼叫 **CancelUpdate** 方法時加入新的資料列，目前的資料列會變成 **AddNew** 呼叫之前的資料列。  
  
 如果您未變更目前的資料列或加入新的資料列，則呼叫 **CancelUpdate** 方法會產生錯誤。
