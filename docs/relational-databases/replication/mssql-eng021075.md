---
title: "MSSQL_ENG021075 | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_ENG021075 錯誤"
ms.assetid: c8c29543-d1f6-49d5-b6c8-e8c3aa373090
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# MSSQL_ENG021075
    
## 訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|21075|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|發行集 '%s' 的初始快照集尚無法使用。|  
  
## 說明  
 如果在「快照集代理程式」完成快照集的產生之前啟動「散發代理程式」或「合併代理程式」，會引發錯誤 MSSQL_ENG021075。  
  
## 使用者動作  
 如果在建立訂閱或上次選擇重新初始化訂閱後未啟動發行集的「快照集代理程式」，請啟動「快照集代理程式」，並讓其在啟動「散發代理程式」或「合併代理程式」之前完成。 如需詳細資訊，請參閱 [建立並套用快照集](../../relational-databases/replication/create-and-apply-the-snapshot.md)。  
  
 若快照集代理程式未完成，請檢查快照集代理程式記錄，以便找出錯誤並加以解決。 複寫監視器中檢視代理程式狀態和錯誤詳細資料的相關資訊，請參閱 [檢視資訊並執行工作的代理程式相關聯的發行集與 #40。複寫監視器 & #41;](../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md)。  
  
 若錯誤繼續發生，請增加代理程式的記錄，並指定記錄的輸出檔。 視錯誤內容的不同，可提供導致錯誤的步驟和 (或) 其他錯誤訊息。  
  
## 另請參閱  
 [錯誤和事件參考 & #40。複寫 & #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  