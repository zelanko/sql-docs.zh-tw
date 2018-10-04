---
title: Transactions 事件類別 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- SQL Server event classes, Transactions event category
- event classes [SQL Server], Transactions event category
- Transactions event category [SQL Server]
ms.assetid: bfc75c5b-7115-49d8-9148-a0c84ee66a9a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e7ab7460d6e94c5bcaffbceb9fe4427e4616d8f3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48050358"
---
# <a name="transactions-event-category"></a>Transaction 事件類別目錄
  **Transactions** 事件類別可以用來監視交易狀態。 以 **TM:** 作為前置詞的事件類別名稱是用來追蹤與交易相關的作業，這些作業是透過交易管理介面來傳送。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[DTCTransaction 事件類別](dtctransaction-event-class.md)|追蹤 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散式交易協調器 (MS DTC) 所協調的交易。 這些是散發於 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的二或多個資料庫或執行個體之間的交易。|  
|[SQLTransaction 事件類別](sqltransaction-event-class.md)|追蹤 [!INCLUDE[tsql](../../includes/tsql-md.md)] BEGIN TRAN、COMMIT TRAN、SAVE TRAN 與 ROLLBACK TRAN 陳述式。|  
|[TM: Begin Tran Completed 事件類別](tm-begin-tran-completed-event-class.md)|表示已完成 BEGIN TRANSACTION 要求。|  
|[TM: Begin Tran Starting 事件類別](tm-begin-tran-starting-event-class.md)|表示正在啟動 BEGIN TRANSACTION 要求。|  
|[TM: Commit Tran Completed 事件類別](tm-commit-tran-completed-event-class.md)|表示已完成 COMMIT TRANSACTION 要求。|  
|[TM: Commit Tran Starting 事件類別](tm-commit-tran-starting-event-class.md)|表示正在啟動 COMMIT TRANSACTION 要求。|  
|[TM: Promote Tran Completed 事件類別](tm-promote-tran-completed-event-class.md)|表示已完成 PROMOTE TRANSACTION 要求。|  
|[TM: Promote Tran Starting 事件類別](tm-promote-tran-starting-event-class.md)|表示正在啟動 PROMOTE TRANSACTION 要求。|  
|[TM: Rollback Tran Completed 事件類別](tm-rollback-tran-completed-event-class.md)|表示已完成 ROLLBACK TRANSACTION 要求。|  
|[TM: Rollback Tran Starting 事件類別](tm-rollback-tran-starting-event-class.md)|表示正在啟動 ROLLBACK TRANSACTION 要求。|  
|[TM: Save Tran Completed 事件類別](tm-save-tran-completed-event-class.md)|表示已完成 SAVE TRANSACTION 要求。|  
|[TM: Save Tran Starting 事件類別](tm-save-tran-starting-event-class.md)|表示正在啟動 SAVE TRANSACTION 要求。|  
|[TransactionLog 事件類別](transactionlog-event-class.md)|追蹤交易何時寫入資料庫交易記錄檔。|  
  
  
