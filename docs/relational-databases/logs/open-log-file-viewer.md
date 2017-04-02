---
title: "開啟記錄檔檢視器 | Microsoft Docs"
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
  - "記錄檔檢視器, 開啟"
ms.assetid: a86b89cb-0432-4648-895a-05ecc5450e45
caps.latest.revision: 29
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 29
---
# 開啟記錄檔檢視器
  您可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中使用記錄檔檢視器，以存取下列記錄中所擷取之錯誤和事件的相關資訊：  
  
-   稽核集合  
  
-   資料收集  
  
-   Database Mail  
  
-   作業記錄  
  
-   SQL Server  
  
-   SQL Server Agent  
  
-   Windows 事件 (這些 Windows 事件也可以從事件檢視器存取)。  
  
 從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 開始，您就可以使用 [已註冊的伺服器] 來檢視本機或遠端 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記錄檔。 當這些執行個體在線上或離線時，您可以使用 [已註冊的伺服器] 來檢視記錄檔。 如需線上存取的詳細資訊，請參閱本主題稍後的＜從已註冊的伺服器檢視線上記錄檔＞程序。 如需如何存取離線 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記錄檔的詳細資訊，請參閱[檢視離線記錄檔](../../relational-databases/logs/view-offline-log-files.md)。  
  
 您可以用許多方式來開啟記錄檔檢視器，端視想要檢視的資訊而定。  
  
##  <a name="BeforeYouBegin"></a> Permissions  
 若要存取線上 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的記錄檔，需要 securityadmin 固定伺服器角色的成員資格。  
  
 若要存取離線 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的記錄檔，您必須具有 **Root\Microsoft\SqlServer\ComputerManagement10** WMI 命名空間以及儲存記錄檔之資料夾的讀取權限。 如需詳細資訊，請參閱[檢視離線記錄檔](../../relational-databases/logs/view-offline-log-files.md)主題的＜安全性＞一節。  
  
### 安全性  
 需要 securityadmin 固定伺服器角色中的成員資格。  
  
### 檢視記錄檔  
  
##### 若要檢視與一般 SQL Server 活動相關的記錄檔  
  
1.  在物件總管中，展開 [管理]。  
  
2.  執行下列任一步驟：  
  
    -   以滑鼠右鍵按一下 [SQL Server 記錄檔]，指向 [檢視]，然後按一下 [SQL Server 記錄檔] 或 [SQL Server 與 Windows 記錄檔]。  
  
    -   展開 [SQL Server 記錄檔]，以滑鼠右鍵按一下任何記錄檔，然後按一下 [檢視 SQL Server 記錄檔]。 您也可以按兩下任何記錄檔。  
  
     這些記錄檔包含 [Database Mail]、[SQL Server]、[SQL Server Agent] 和 [Windows NT]。  
  
##### 若要檢視與作業相關的記錄檔  
  
-   在物件總管中，展開 [SQL Server Agent]，以滑鼠右鍵按一下 [作業]，然後按一下 [檢視記錄]。  
  
     這些記錄檔包含 [Database Mail]、[作業記錄] 和 [SQL Server Agent]。  
  
##### 若要檢視與維護計畫相關的記錄檔  
  
-   在物件總管中，展開 [管理]，以滑鼠右鍵按一下 [維護計畫]，然後按一下 [檢視記錄]。  
  
     這些記錄檔包含 [Database Mail]、[作業記錄]、[維護計畫]、[遠端維護計畫] 和 [SQL Server Agent]。  
  
##### 若要檢視與資料收集相關的記錄檔  
  
-   在物件總管中，展開 [管理]，以滑鼠右鍵按一下 [資料收集]，然後按一下 [檢視記錄]。  
  
     這些記錄檔包含 [資料收集]、[作業記錄] 和 [SQL Server Agent]。  
  
##### 若要檢視與 Database Mail 相關的記錄檔  
  
-   在物件總管中，展開 [管理]，以滑鼠右鍵按一下 [Database Mail]，然後按一下 [檢視 Database Mail 記錄]。  
  
     這些記錄檔包含 [Database Mail]、[作業記錄]、[維護計畫]、[遠端維護計畫]、[SQL Server]、[SQL Server Agent] 和 [Windows NT]。  
  
##### 若要檢視與稽核收集相關的記錄檔  
  
-   在物件總管中，依序展開 [安全性] 和 [稽核]，以滑鼠右鍵按一下稽核，然後按一下 [檢視稽核記錄]。  
  
     這些記錄檔包含 [稽核收集] 和 [Windows NT]。  
  
##### 若要檢視與稽核收集相關的記錄檔  
  
-   在物件總管中，依序展開 [安全性] 和 [稽核]，以滑鼠右鍵按一下稽核，然後按一下 [檢視稽核記錄]。  
  
     這些記錄檔包含 [稽核收集] 和 [Windows NT]。  
  
## 另請參閱  
 [記錄檔檢視器](../../relational-databases/logs/log-file-viewer.md)   
 [SQL Server Audit &#40;Database Engine&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)   
 [檢視離線記錄檔](../../relational-databases/logs/view-offline-log-files.md)  
  
  