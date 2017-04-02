---
title: "修改 SQL Server R 服務的使用者帳戶集區 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 58b79170-5731-46b5-af8c-21164d28f3b0
caps.latest.revision: 19
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# 修改 SQL Server R 服務的使用者帳戶集區
  安裝程序的一部分 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], ，新的 Windows *使用者帳戶的集區* 為了支援執行工作所 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服務。 這些背景工作帳戶的用途是隔離並行執行的 R 指令碼，由不同的 SQL 使用者。
  
  這個集區的使用者帳戶數目會決定可以同時啟用多少個 R 工作階段。   如果同一個使用者同時執行多個 R 指令碼，所有由該使用者所執行的工作階段將使用相同的工作帳戶。 因此，單一使用者可能有 100 不同 R 指令碼執行同時的長度不允許的資源。

## 預設組態   
-   預設執行個體中的群組名稱是 **SQLRUserGroup**。 
-   具名執行個體，在預設的群組名稱的後置字元的執行個體名稱︰ 例如， **SQLRUserGroupMyInstanceName**。 
-   帳戶︰ 根據預設，使用者帳戶集區包含 20 個使用者帳戶，名為 **MSSQLSERVER01** 透過 **MSSQLSERVER20** 預設執行個體。  
-   對於具名執行個體，使用者帳戶使用命名的執行個體名稱︰ 例如， **MyInstanceName01** 透過 **MyInstanceName20**。  


## 每個執行個體管理使用者群組
Windows 帳戶群組由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] R 服務已安裝的所以如果您已安裝支援 R 的多個執行個體，不會有多個使用者群組每個執行個體的安裝。
不過，每個使用者群組相關聯 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服務上的特定執行個體，而且不支援在其他執行個體執行的 R 工作。

根據預設，群組沒有 **不** 擁有登入權限 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與它在相關聯的執行個體。 如果您必須啟用使用者的 R 指令碼執行，資料庫管理員必須提供此群組 **連接到** 權限。  

### 變更 Windows 使用者群組中的背景工作帳戶數目

若要修改的帳戶集區中的使用者數目，您必須編輯的屬性 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服務，如下所述。  
  
每個使用者帳戶相關聯的密碼產生隨機，但是您之後可以變更這些帳戶建立之後。  
  
1. 開啟 SQL Server 組態管理員，然後選取 **SQL Server 服務**。
2. 按兩下 [SQL Server Launchpad 服務，如果它正在停止服務。 
3.  在 **服務** 索引標籤，確定 [啟動模式] 設定為自動。 如果未執行 [啟動列]，R 指令碼將會失敗。
4.  按一下 [ **進階** 標籤，然後編輯的值 **外部使用者計數** 如有必要。 此設定會控制多少不同的 SQL 使用者可以同時執行查詢，在。預設為 20 個帳戶，在大多數情況下為多個適合用來支援 R 工作階段。
5. （選擇性） 您可以設定選項 **重設密碼的外部使用者** 至 _是_ 如果您的組織有需要變更密碼每隔 90 天的規則。 執行此動作會重新產生加密啟動列維護使用者帳戶的密碼。    
6.  重新啟動服務。  

## 遠端指令碼執行所需的其他權限
如果您執行 R 指令碼，與為遠端 SQL Server 電腦計算內容，這個背景工作群組需要登入 SQL Server 執行個體將會執行 R 指令碼的權限。

如需詳細資訊，請參閱 [升級與安裝的常見問題集](../../advanced-analytics/r-services/upgrade-and-installation-faq-sql-server-r-services.md)。 

  
## 另請參閱  
 [組態 (SQL Server R Services)](../../advanced-analytics/r-services/configuration-sql-server-r-services.md)
  