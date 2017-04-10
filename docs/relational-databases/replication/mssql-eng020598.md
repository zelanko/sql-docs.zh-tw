---
title: "MSSQL_ENG020598 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_ENG020598 錯誤"
ms.assetid: 1c3032f2-23d1-4ead-94ee-16ac4d75cd0c
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# MSSQL_ENG020598
    
## 訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|20598|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|套用複寫命令時，在訂閱者端找不到資料列。|  
  
## 說明  
 如果「散發代理程式」嘗試在「訂閱者」端更新資料列，但該資料列已刪除或其主索引鍵已變更，則會在異動複寫中發生這項錯誤。 依預設，交易式發行集的訂閱者應當成唯讀處理，因為變更並不會傳播回發行者。 針對異動複寫，只有在使用可更新訂閱或點對點複寫時，才應於「訂閱者」端進行使用者變更。 這些選項的相關資訊，請參閱 [交易式複寫的可更新訂閱](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md) 和 [端對端交易式複寫](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。  
  
## 使用者動作  
 **若要解決這個問題：**  
  
1.  如果複寫必須繼續在您找到錯誤的來源時，請指定參數 **-SkipErrors 20598** 「 散發代理程式。 這可以讓代理程式略過導致錯誤 20598 的變更，同時允許複寫其他變更。  
  
2.  識別「訂閱者」端的哪些資料列已刪除，或擁有與「發行者」端對應的資料列不同的主索引鍵。 您可以使用 [tablediff Utility](../../tools/tablediff-utility.md) 判斷發行集和訂閱資料庫中不同的資料列。 使用此公用程式與複寫資料庫的相關資訊，請參閱 [比較複寫資料表差異 & #40。複寫程式設計 & #41;](../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md)。  
  
3.  在「訂閱者」端使用 **tablediff** 公用程式或其他方法更正資料列。  
  
4.  （選擇性）移除 **-SkipErrors** 參數。  
  
## 另請參閱  
 [錯誤和事件參考 & #40。複寫 & #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  