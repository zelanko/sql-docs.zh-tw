---
title: "建立效能基準 | Microsoft Docs"
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
  - "資料庫效能 [SQL Server], 基準"
  - "監視效能 [SQL Server], 基準"
  - "微調資料庫 [SQL Server], 基準"
  - "伺服器效能 [SQL Server], 基準"
  - "效能 [SQL Server], 基準"
  - "基準效能 [SQL Server]"
  - "基準線統計資料的度量單位 [SQL Server]"
  - "監視伺服器效能 [SQL Server], 建立基準"
  - "資料庫監視 [SQL Server], 基準"
ms.assetid: dc5aa8d6-2507-448f-ad86-4196443915fc
caps.latest.revision: 22
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 22
---
# 建立效能基準
  若要判斷您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統是否以最佳方式執行，請長時間定期測量效能 (即使沒有問題發生)，以建立伺服器效能基準。 請將每個新的組測量的結果與先前的測量進行比較。  
  
 以下各方面會影響 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的效能：  
  
-   系統資源 (硬體)  
  
-   網路架構  
  
-   作業系統  
  
-   資料庫應用程式  
  
-   用戶端應用程式  
  
 至少需使用基準線測量來判斷：  
  
-   作業的尖峰與離峰期間。  
  
-   產生查詢或批次命令的回應時間。  
  
-   資料庫備份與還原的完成時間。  
  
 建立伺服器效能基準線之後，請將基準線統計資料表與目前的伺服器效能進行比較。 與基準線差距過高或過低的數值即為必須進一步調查的候選項目。 這些項目可能代表必須調整或重設設定的範圍。 例如，當執行一組查詢的時間量增加時，請檢查查詢以判斷是否可以重寫查詢，或者是否必須加入資料行統計資料或新的索引。  
  
## 另請參閱  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  