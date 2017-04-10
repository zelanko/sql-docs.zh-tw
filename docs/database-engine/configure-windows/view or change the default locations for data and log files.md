---
title: "檢視或變更資料及記錄檔的預設位置 (SQL Server Management Studio) | Microsoft Docs"
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
  - "記錄檔 [SQL Server], 變更預設位置"
  - "資料檔 [SQL Server], 變更預設位置"
ms.assetid: 70a57fda-fcfe-490f-9cf6-5df620e32b2a
caps.latest.revision: 16
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
---
# 檢視或變更資料及記錄檔的預設位置 (SQL Server Management Studio)
  此主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中檢視和變更新資料和記錄檔的預設位置。 預設路徑是從登錄取得。 在變更位置之後，如果未指定不同的位置， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中建立的所有新資料庫都會使用該位置。  
  
 
##  <a name="Recommendations"></a> 建議  
 保護資料檔和記錄檔的最佳作法是確定它們受到存取控制清單 (ACL) 所保護。 在建立這些檔案的根目錄下設定 ACL。  
  
  
## 檢視或變更資料庫檔案的預設位置  
  
1.  在物件總管中，以滑鼠右鍵按一下伺服器，然後按一下 [屬性]。  
  
2.  在該 [屬性] 頁面的左面板中，按一下 [資料庫設定] 索引標籤。  
  
3.  在 **[資料庫預設位置]**中，您可以檢視新資料檔和新記錄檔的目前預設位置。 若要變更預設位置，在 **[資料]** 或 **[記錄]** 欄位中輸入新的預設路徑名稱，或按一下 [瀏覽] 按鈕來尋找並選取路徑名稱。  
  
>**注意：**變更預設位置之後，您必須停止並啟動 SQL Server 服務，才能完成變更。  
  
## 另請參閱  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [建立資料庫](../../relational-databases/databases/create-a-database.md)  
  
  