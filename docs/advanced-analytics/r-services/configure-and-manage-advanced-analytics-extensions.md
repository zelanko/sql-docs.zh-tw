---
title: "設定及管理進階分析擴充功能 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "11/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8d73fd98-0c61-4a62-94bb-75658195f2a6
caps.latest.revision: 21
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 20
---
# 設定及管理進階分析擴充功能
  在安裝 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]後，您可以在 R 執行階段及其他 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 相關服務的組態中進行微幅變更。  
  
  
 **本主題內容**  
  
-   [為 SQL Server R Services 佈建使用者帳戶](#bkmk_Provisioning)  
  
-   [管理 R 處理序的記憶體使用](#bkmk_ManagingMemory)  
  
-   [使用組態檔變更服務預設](#bkmk_ChangingConfig) 

-   [修改 Launchpad 服務帳戶](#bkmk_Launchpad) 
  
##  <a name="bkmk_Provisioning"></a> 為 SQL Server R Services 佈建使用者帳戶  
 R 執行階段中處理程序 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 低權限的本機使用者帳戶內容中執行。 以個別的低權限帳戶執行 R 執行階段處理序有以下好處：  
  
-   降低 R 執行階段處理序在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦上執行的權限。  
  
-   讓 R 執行階段工作階段彼此隔離  
  
 在安裝程序的一部分 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], ，新的 Windows *使用者帳戶的集區* 建立，其中包含執行 R 執行階段程序所需的本機使用者帳戶。 您可以修改使用者的數目，如果需要支援。您的資料庫管理員也必須提供此群組的權限連接到任何已啟用 R 服務的執行個體。 如需詳細資訊，請參閱 [修改使用者帳戶集區的 SQL Server R Services](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md)。  
  
 不過，存取控制清單 (ACL) 可以定義機密資源 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 拒絕存取此群組來讓 R 執行階段處理序無法取得資源的存取權。  
  
-   使用者帳戶集區會連結到特定的執行個體。  每個執行個體已啟用的指令碼，另一個背景工作集區會建立帳戶。 無法執行個體之間共用帳戶。
  
-   集區中的使用者帳戶名稱格式為 SQLInstanceName*nn*。 例如，如果您使用預設執行個體作為您的 R 伺服器，使用者帳戶集區即支援 MSSQLSERVER01、MSSQLSERVER02 等帳戶名稱。  
  
-   使用者帳戶集區的大小為靜態，預設值是 20。 可同時啟動的 R 執行階段工作階段數目受限於此使用者帳戶集區大小。 不過，這項限制可使用 SQL Server 組態管理員變更由系統管理員。  
  
  
 如需如何對使用者帳戶集區進行變更的詳細資訊，請參閱 [Modify the User Account Pool for SQL Server R Services](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md)。  
  
##  <a name="bkmk_ManagingMemory"></a> 管理 R 處理序的記憶體使用  
 根據預設，與 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 相關聯的 R 執行階段處理序不得使用 20% 以上的機器總記憶體。 不過，系統管理員可以在需要時提高此限制。  
  
 一般而言，這個數量將會用於嚴重的 R 工作，例如訓練模型或預測多個資料列的資料上。 您可能需要保留的記憶體減少 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （或其他服務），用以定義外部的資源集區或集區和配置的資源管理員。 如需詳細資訊，請參閱 [R 服務的資源控管](../../advanced-analytics/r-services/resource-governance-for-r-services.md)。  
  
##  <a name="bkmk_ChangingConfig"></a> 變更進階服務選項使用組態檔  
 
您可以控制某些進階的屬性 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 藉由編輯 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 組態檔。 此檔案建立於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝期間，並且預設會以純文字檔案儲存在以下位置：  
 
```  
<instance path>\binn\rlauncher.config  
```  
  
 您必須在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的電腦上身為系統管理員，才能對此檔案進行變更。 如果您編輯了檔案，建議您在儲存變更前先備份副本。  
  
 例如，若要使用記事本開啟預設執行個體 (MSSQLSERVER) 的組態檔，您會以系統管理員身分開啟命令提示字元，然後鍵入以下命令：  
  
```  
C:\>Notepad.exe "%programfiles%\Microsoft SQL Server\MSSQL13.MSSQLSERVER\mssql\binn\rlauncher.config"  
  
```  
  
###  <a name="bkmk_properties"></a> 組態屬性  
 所有設定都會採用機碼值組的格式，分別位於獨立的行。 例如，此屬性會指定 R 處理序不得使用 20% 以上的系統記憶體：  
  
 預設： `MEMORY_LIMIT_PERCENT=20`  
  
 下表列出每個設定，支援 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], ，所允許的值。  
  
|設定名稱|值類型|預設值|描述|  
|------------------|----------------|-------------|-----------------|  
|JOB_CLEANUP_ON_EXIT|Integer<br /><br /> 0 = 已停用<br /><br /> 1 = 已啟用|1<br /><br /> 記錄檔會在結束時移除|指定是否在 R 工作階段完成後清理為每個 R 工作建立的暫存工作資料夾。 這項設定在偵錯時很有用。<br /><br /> 注意：這只是內部設定，請勿變更此值。|  
|TRACE_LEVEL|Integer<br /><br /> 1 = 錯誤<br /><br /> 2 = 效能<br /><br /> 3 = 警告<br /><br /> 4 = 資訊|1<br /><br /> 僅輸出警告|設定 R 啟動程式 (MSSQLLAUNCHPAD) 的追蹤詳細資訊層級以進行偵錯。 此設定會影響下列追蹤檔案中儲存的追蹤詳細資訊層級，兩者均位於 LOG_DIRECTORY 設定指定的路徑：<br /><br /> **rlauncher.log**: R 工作階段啟動 T-SQL 查詢所產生的追蹤檔案。<br /><br /> 如需此案例的詳細資訊，請參閱 [Data Exploration and Predictive Modeling with R](../../advanced-analytics/r-services/data-exploration-and-predictive-modeling-with-r.md)。|  

## <a name="bkmk_Launchpad"></a>修改 Launchpad 服務帳戶

個別 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 服務會為您已設定每個執行個體建立 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]。 

根據預設，[啟動列] 被設定為使用 NT Service\MSSQLLaunchpad，所有必要的權限執行 R 指令碼將會佈建帳戶執行。 不過，如果您變更此帳戶時，[啟動列] 可能無法啟動或存取 SQL Server 執行個體執行 R 指令碼的位置。
 
  如果您修改服務帳戶，務必使用 **本機安全性原則** 應用程式，並更新每個服務的權限帳戶包含這些權限︰
  + 調整處理序的記憶體配額 (SeIncreaseQuotaPrivilege)
  + 略過跨越檢查 (SeChangeNotifyPrivilege)
  + 以服務登入 (SeServiceLogonRight)
  + 取代處理序層級 Token (SeAssignPrimaryTokenPrivilege)

如需有關執行 SQL Server 服務所需的權限的詳細資訊，請參閱 [設定 Windows 服務帳戶和權限](https://msdn.microsoft.com/library/ms143504.aspx#Windows)。
   
## 另請參閱  
 [SQL Server R 服務使用者入門](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)  
  
  