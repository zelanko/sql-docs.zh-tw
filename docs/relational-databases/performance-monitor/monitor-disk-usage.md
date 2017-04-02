---
title: "監視磁碟使用量 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "資料庫監視 [SQL Server], 磁碟使用量"
  - "磁碟 [SQL Server]"
  - "監視效能 [SQL Server], 磁碟使用量"
  - "伺服器效能 [SQL Server], 磁碟使用量"
  - "監視 [SQL Server], 磁碟活動"
  - "超過分頁 [SQL Server]"
  - "微調資料庫 [SQL Server], 磁碟使用量"
  - "I/O [SQL Server], 監視"
  - "磁碟 [SQL Server], 監視活動"
  - "隔離磁碟活動 [SQL Server]"
  - "資料庫效能 [SQL Server], 磁碟使用量"
  - "監視伺服器效能 [SQL Server], 磁碟使用量"
ms.assetid: 1525449c-ea7d-4222-b294-1ba1fe99c9ac
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# 監視磁碟使用量
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用 Microsoft Windows 作業系統輸入/輸出 (I/O) 呼叫，在您的磁碟上執行讀取和寫入作業。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會管理何時及如何執行磁碟 I/O，但是 Windows 作業系統會執行基礎 I/O 作業。 I/O 子系統包含了系統匯流排、磁碟控制卡、磁碟、磁帶機、光碟機和許多其他的 I/O 裝置。 磁碟 I/O 經常是造成系統瓶頸的原因。  
  
 監視磁碟活動涉及兩個重點：  
  
-   監視磁碟 I/O 與偵測額外的分頁方式  
  
-   隔離 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 建立的磁碟活動  
  
 如需詳細資訊，請參閱 [監視磁碟使用量](http://social.technet.microsoft.com/wiki/contents/articles/monitoring-disk-usage.aspx)  
  
  