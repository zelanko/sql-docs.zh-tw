---
title: "進階組態選項的機器學習服務 |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 11/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8d73fd98-0c61-4a62-94bb-75658195f2a6
caps.latest.revision: 21
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 872acf107d72989b4623a9d5f4ccb85c44d1f2f9
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="advanced-configuration-options-for-machine-learning-services"></a>進階機器學習服務的設定選項

本文描述您可以在安裝之後，若要修改 R 執行階段和其他 SQL Server 中的機器學習服務相關聯的服務組態進行的變更。

適用於： SQL Server 2016 R Services、 SQL Server 2017 機器學習服務

##  <a name="bkmk_Provisioning"></a>佈建使用者帳戶的機器學習

中的外部指令碼處理序[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]低權限本機使用者帳戶內容中執行。 在個別的低權限帳戶中執行這些程序有下列優點：

+ 降低的外部指令碼執行階段處理序的權限上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]電腦
+ 提供例如 R 或 Python 的外部執行階段的工作階段之間的隔離。

在新的 Windows 安裝程序，為*使用者帳戶集區*建立，其中包含執行 R 執行階段程序所需的本機使用者帳戶。 您可以視需要修改使用者的數目以支援 R。您的資料庫管理員也必須賦予此群組權限以連線到已啟用 R Services 的任何執行個體。 如需詳細資訊，請參閱 [Modify the User Account Pool for SQL Server R Services](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)相關服務的組態中進行微幅變更。

不過，您可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 對機密資源定義存取控制清單 (ACL)，以拒絕此群組的存取權，進而防止 R 執行階段處理序取得資源存取權。

+ 使用者帳戶集區會連結到特定的執行個體。  已啟用 R 指令碼的每個執行個體，都會建立另外一個背景工作帳戶集區。 執行個體之間的帳戶無法共用。

+ 集區中的使用者帳戶名稱格式為 SQLInstanceName*nn*相關服務的組態中進行微幅變更。 例如，如果您使用預設執行個體作為您的 R 伺服器，使用者帳戶集區即支援 MSSQLSERVER01、MSSQLSERVER02 等帳戶名稱。

+ 使用者帳戶集區的大小為靜態，預設值是 20。 可同時啟動的 R 執行階段工作階段數目受限於此使用者帳戶集區大小。 不過，系統管理員可以使用 SQL Server 組態管理員變更這項限制。

如需如何對使用者帳戶集區進行變更的詳細資訊，請參閱 [Modify the User Account Pool for SQL Server R Services](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)。

##  <a name="bkmk_ManagingMemory"></a>管理外部指令碼處理序所使用的記憶體

根據預設，與 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 相關聯的 R 執行階段處理序不得使用 20% 以上的機器總記憶體。 不過，系統管理員可以在需要時提高此限制。

一般而言，這個數量對於負荷較重的 R 工作 (例如訓練模型或針對多個資料列進行預測) 不太足夠。 您可能需要減少針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (或其他服務) 所保留的記憶體，並使用 Resource Governor 定義外部資源集區和配置。 如需詳細資訊，請參閱[資源管理針對 R](../../advanced-analytics/r/resource-governance-for-r-services.md)。

##  <a name="bkmk_ChangingConfig"></a>變更進階服務選項使用組態檔

您可以編輯 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 組態檔來控制 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的某些進階屬性。 此檔案建立於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝期間，並且預設會以純文字檔案儲存在以下位置：

`<instance path>\binn\rlauncher.config`

您必須在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的電腦上身為系統管理員，才能對此檔案進行變更。 如果您編輯了檔案，建議您在儲存變更前先備份副本。

例如，若要使用 記事本 開啟組態檔的預設執行個體，會開啟 命令提示字元，以系統管理員身分，並輸入下列命令：

```
C:\>Notepad.exe "%programfiles%\Microsoft SQL Server\MSSQL13.MSSQLSERVER\mssql\binn\rlauncher.config"  
```

##  <a name="bkmk_properties"></a>編輯組態屬性

下表列出 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 支援的各項設定，並附有允許的值。

所有設定都會採用機碼值組的格式，分別位於獨立的行。 例如，這個屬性指定 RLauncher 的追蹤層級：

預設值︰TRACE_LEVEL=4


|**設定名稱**|**值類型**|**預設值**|**描述**|
|------------------|----------------|-------------|-----------------|
|JOB_CLEANUP_ON_EXIT|Integer<br /><br /> 0 = 已停用<br /><br /> 1 = 已啟用|1<br /><br /> 記錄檔會在結束時移除|指定是否在 R 工作階段完成後清理為每個 R 工作建立的暫存工作資料夾。 這項設定在偵錯時很有用。<br /><br /> 注意：這只是內部設定，請勿變更此值。|
|TRACE_LEVEL|Integer<br /><br /> 1 = 錯誤<br /><br /> 2 = 效能<br /><br /> 3 = 警告<br /><br /> 4 = 資訊|1<br /><br /> 僅輸出警告|設定 R 啟動程式 (MSSQLLAUNCHPAD) 的追蹤詳細資訊層級以進行偵錯。 此設定會影響下列追蹤檔案中儲存的追蹤詳細資訊層級，兩者均位於 LOG_DIRECTORY 設定指定的路徑：<br /><br /> **rlauncher.log**：為 T-SQL 查詢啟動的 R 工作階段產生的追蹤檔案。<br /><br /> |

## <a name="bkmk_Launchpad"></a>修改 Launchpad 服務帳戶

個別[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]每個執行個體，您已設定機器學習服務建立服務。

根據預設，Launchpad 會設定為使用 NT Service\MSSQLLaunchpad 帳戶執行，此帳戶已佈建執行 R 指令碼所有必要的權限。 不過，如果您變更此帳戶時，[啟動列] 可能無法啟動，或存取 SQL Server 執行個體應在何處執行外部指令碼。

如果您要修改服務帳戶，請務必使用「本機安全性原則」應用程式並更新每個服務帳戶的權限以包含這些權限︰

+ 調整處理序的記憶體配額 (SeIncreaseQuotaPrivilege)
+ 略過跨越檢查 (SeChangeNotifyPrivilege)
+ 以服務登入 (SeServiceLogonRight)
+ 取代處理序層級 Token (SeAssignPrimaryTokenPrivilege)

如需執行 SQL Server 服務所需權限的詳細資訊，請參閱[設定 Windows 服務帳戶與權限](https://msdn.microsoft.com/library/ms143504.aspx#Windows)。

## <a name="see-also"></a>另請參閱

[安全性考量](security-considerations-for-the-r-runtime-in-sql-server.md)
