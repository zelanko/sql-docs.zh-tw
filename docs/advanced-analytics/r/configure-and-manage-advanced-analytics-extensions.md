---
title: SQL Server 機器學習服務的進階的組態 |Microsoft 文件
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 5fc4e661f68a23ff2a954b832463eb60c7449057
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="advanced-configuration-options-for-sql-server-machine-learning-services"></a>SQL Server 機器學習服務的進階的組態選項
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文描述您可以在安裝之後，若要修改外部指令碼執行階段和其他 SQL Server 中的機器學習服務相關聯的服務組態進行的變更。

**適用於：** SQL Server 2016 R Services、 SQL Server 2017 機器學習服務

##  <a name="bkmk_Provisioning"></a> 佈建額外的使用者帳戶的機器學習

中的外部指令碼處理序[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]低權限本機使用者帳戶內容中執行。 在個別的低權限帳戶中執行這些程序有下列優點：

+ 降低的外部指令碼執行階段處理序的權限上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]電腦
+ 提供例如 R 或 Python 的外部執行階段的工作階段之間的隔離。

在新的 Windows 安裝程序，為*使用者帳戶集區*建立，其中包含執行外部執行階段處理序，例如 R 或 Python 所需的本機使用者帳戶。 您可以修改使用者的數目，視需要以支援機器學習工作。 

此外，您的資料庫管理員必須授與此群組權限連接到機器學習中已啟用的任何執行個體。 如需詳細資訊，請參閱[修改使用者帳戶集區的 SQL Server 機器學習服務](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)。

在 protext 敏感資源[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您可以定義這個群組的存取控制清單 (ACL)。 藉由指定該群組被拒絕存取的資源，您可以避免存取外部處理序的 R 或 Python 執行階段，例如。

+ 使用者帳戶集區會連結到特定的執行個體。 Machine learning 已啟用每個執行個體需要不同的集區的背景工作帳戶。 執行個體之間的帳戶無法共用。

+ 集區中的使用者帳戶名稱格式為 SQLInstanceName*nn*。 例如，如果您使用預設執行個體為機器學習服務，使用者帳戶集區支援 MSSQLSERVER01、 mssqlserver02 等帳戶名稱。

+ 使用者帳戶集區的大小為靜態，預設值是 20。 可同時啟動的外部執行階段工作階段數目受限於此使用者帳戶集區的大小。 若要變更此限制，系統管理員應該使用 SQL Server 組態管理員。

如需如何變更使用者帳戶集區的詳細資訊，請參閱[修改使用者帳戶集區的 SQL Server 機器學習服務](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)。

##  <a name="bkmk_ManagingMemory"></a> 管理外部指令碼處理序所使用的記憶體

根據預設，機器學習的外部指令碼執行階段會限制為不超過 20%的機器總記憶體。 這取決於您的系統，但一般而言，您可能會發現這項限制不足以嚴重的機器學習工作，例如模型定型或預測多個資料列的資料上。 

若要支援機器學習，系統管理員可以增加此限制。 當您這樣做時，您可能需要降低為保留的記憶體數量[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或其他服務。 您也應該考慮使用資源管理員定義外部資源集區或集區，以便您可以配置給 R 或 Python 工作特定的資源集區。

如需詳細資訊，請參閱[機器學習資源控管](../../advanced-analytics/r/resource-governance-for-r-services.md)。


## <a name="bkmk_Launchpad"></a>修改啟動控制板服務帳戶

個別[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]每個執行個體，您已設定機器學習服務建立服務。

根據預設，Launchpad 會設定為使用 NT Service\MSSQLLaunchpad 帳戶執行，此帳戶已佈建執行 R 指令碼所有必要的權限。 不過，如果您變更此帳戶時，[啟動列] 可能無法啟動，或存取 SQL Server 執行個體應在何處執行外部指令碼。

如果您要修改服務帳戶，請務必使用「本機安全性原則」應用程式並更新每個服務帳戶的權限以包含這些權限︰

+ 調整處理序的記憶體配額 (SeIncreaseQuotaPrivilege)
+ 略過跨越檢查 (SeChangeNotifyPrivilege)
+ 以服務登入 (SeServiceLogonRight)
+ 取代處理序層級 Token (SeAssignPrimaryTokenPrivilege)

如需執行 SQL Server 服務所需權限的詳細資訊，請參閱[設定 Windows 服務帳戶與權限](https://msdn.microsoft.com/library/ms143504.aspx#Windows)。

##  <a name="bkmk_ChangingConfig"></a> 變更進階的服務選項

在早期版本的 SQL Server 2016 R 服務，您無法變更服務的某些屬性，藉由編輯[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]組態檔。 

不過，這個檔案不再用來變更設定。 我們建議您在服務組態，例如服務帳戶和使用者人數效果變更使用 SQL Server 組態管理員。

**若要修改 [啟動列] 設定**

1. 開啟 [SQL Server 組態管理員](../../relational-databases/sql-server-configuration-manager.md)。 
2. SQL Server 啟動列 上按一下滑鼠右鍵，然後選取**屬性**。

    + 若要變更服務帳戶，請按一下**登入** 索引標籤。

    + 若要增加的使用者數目，請按一下**進階** 索引標籤。


**若要修改的偵錯設定**

幾個屬性只可以變更使用 [啟動列] 的組態檔，可能會在有限的情況下，例如偵錯很有用。 組態檔建立期間[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]設定，並依預設會儲存為純文字檔案中的下列位置： `<instance path>\binn\rlauncher.config`

您必須在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的電腦上身為系統管理員，才能對此檔案進行變更。 如果您編輯了檔案，建議您在儲存變更前先備份副本。

下表列出的進階的設定[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，以允許的值。 

|**設定名稱**|**型別**|**說明**|
|----|----|----|
|作業\_清除\_ON\_結束|Integer |這是內部設定只，請勿變更此值。 </br></br>指定是否針對每個外部執行階段工作階段建立的暫存工作資料夾應該清除工作階段完成之後。 這項設定在偵錯時很有用。 </br></br>支援的值為**0** （停用） 或**1** （啟用）。 </br></br>預設值為 1，表示記錄檔會在結束時移除。|
|追蹤\_層級|Integer |會追蹤詳細等級的 MSSQLLAUNCHPAD 設定以進行偵錯。 這會影響 LOG_DIRECTORY 設定指定的路徑中的追蹤檔案。 </br></br>支援的值為： **1** （錯誤）， **2** （效能）， **3** （警告） **4** （資訊）。 </br></br>預設值為 1，這表示僅輸出警告。|

所有設定都會採用機碼值組的格式，分別位於獨立的行。 例如，若要變更的追蹤層級，您將加入行`Default: TRACE_LEVEL=4`。

## <a name="see-also"></a>另請參閱

[安全性考量](security-considerations-for-the-r-runtime-in-sql-server.md)
