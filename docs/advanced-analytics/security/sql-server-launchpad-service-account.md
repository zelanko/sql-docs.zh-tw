---
title: SQL Server 受信任的 Launchpad 服務帳戶組態 |Microsoft Docs
description: 如何修改用於 SQL Server 上的外部指令碼執行的 SQL Server 受信任的 Launchpad 服務帳戶。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/27/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 85d96d758d2f363b3b4ec40131723ad10613b64c
ms.sourcegitcommit: 485e4e05d88813d2a8bb8e7296dbd721d125f940
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2018
ms.locfileid: "49100389"
---
# <a name="sql-server-launchpad-service-configuration"></a>SQL Server Launchpad 服務組態
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]是一項服務，負責管理和執行外部指令碼，類似於全文檢索索引及查詢服務啟動個別的主機，來處理全文檢索查詢的方式。

個別[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]建立服務時有加入 SQL Server 機器學習 （R 或 Python） 整合的每個資料庫引擎執行個體。

如需詳細資訊，請參閱中的 [啟動列] 區段[SQL Server Machine Learning 服務中的擴充性架構](../../advanced-analytics/concepts/extensibility-framework.md#launchpad)和[擴充性架構，在 SQL Server Machine Learning 中的安全性概觀服務](../../advanced-analytics/concepts/security.md#launchpad)。

## <a name="account-permissions"></a>帳戶權限

根據預設，SQL Server Launchpad 設定下執行**NT Service\MSSQLLaunchpad**，這將會佈建所有必要的權限執行外部指令碼。 移除此帳戶的權限，可能會導致無法啟動，或存取應在何處執行外部指令碼的 SQL Server 執行個體的啟動列。

如果您修改服務帳戶，務必使用**本機安全性原則**應用程式 (**所有應用程式** > **Windows 系統管理工具** > **本機安全性原則**)。

此帳戶所需的權限詳列於下表。

| 群組原則設定 | 常數的名稱 |
|----------------------|---------------|
| [調整處理序的記憶體配額](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/adjust-memory-quotas-for-a-process) | SeIncreaseQuotaPrivilege | 
| [略過周遊檢查](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/bypass-traverse-checking) | SeChangeNotifyPrivilege | 
| [以服務方式登](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/log-on-as-a-service) | SeServiceLogonRight | 
| [取代處理序層級 token](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/replace-a-process-level-token) | SeAssignPrimaryTokenPrivilege | 

如需執行 SQL Server 服務所需權限的詳細資訊，請參閱[設定 Windows 服務帳戶與權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。

<a name="bkmk_ChangingConfig"></a> 

## <a name="configuration-properties"></a>組態屬性

一般而言，沒有理由来修改服務組態。 無法變更的屬性包含服務帳戶、 的外部處理序 (依預設 20) 或密碼重設原則的背景工作帳戶。

1. 開啟 [SQL Server 組態管理員](../../relational-databases/sql-server-configuration-manager.md)。 

  + 在 [開始] 頁面上輸入**MMC**開啟 Microsoft Management Console。

  + 在 **檔案** > **新增/移除嵌入式管理單元**，移動**SQL Server 組態管理員**從適用於選取的嵌入式管理單元。

2. 在 SQL Server 組態管理員 SQL Server 服務] 下，以滑鼠右鍵按一下 [SQL Server 啟動控制板，然後選取**屬性**。

  + 若要變更服務帳戶，請按一下**登入** 索引標籤。

  + 若要增加的使用者數目，請按一下**進階** 索引標籤。

> [!Note]
> 在舊版的 SQL Server 2016 R Services 中，您可以變更服務的某些屬性，藉由編輯[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]組態檔。 這個檔案不會再用於變更組態。 SQL Server 組態管理員是變更服務組態，例如服務帳戶和使用者人數以正確的方法。

## <a name="debug-settings"></a>偵錯設定

有幾個屬性只可以變更使用 [啟動列] 的組態檔，可能會在有限的情況下，例如偵錯很有用。 組態檔時，就會建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]設定，並依預設會儲存為純文字檔案中的下列位置： `<instance path>\binn\rlauncher.config`

您必須在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的電腦上身為系統管理員，才能對此檔案進行變更。 如果您編輯了檔案，建議您在儲存變更前先備份副本。

下表列出的進階的設定[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，允許的值。 

|**設定名稱**|**型別**|**說明**|
|----|----|----|
|作業\_清理\_ON\_結束|Integer |這是內部設定只，請勿變更此值。 </br></br>指定是否針對每個外部執行階段工作階段建立的暫存工作資料夾清除工作階段完成之後。 這項設定在偵錯時很有用。 </br></br>支援的值為**0** （停用） 或**1** （啟用）。 </br></br>預設值為 1，表示記錄檔會在結束時移除。|
|追蹤\_層級|Integer |設定追蹤的詳細資訊層級 MSSQLLAUNCHPAD 用來偵錯之用。 這會影響 LOG_DIRECTORY 設定指定的路徑中的追蹤檔案。 </br></br>支援的值為： **1** （錯誤）， **2** （效能）， **3** （警告） **4** （資訊）。 </br></br>預設值為 1，這表示僅輸出警告。|

所有設定都會採用機碼值組的格式，分別位於獨立的行。 例如，若要變更的追蹤層級，您將加入行`Default: TRACE_LEVEL=4`。

## <a name="enforcing-password-policy"></a>強制執行密碼原則

如果您的組織要求定期變更密碼，您可能需要強制 Launchpad 服務重新產生為其工作者帳戶維護的加密密碼。

若要啟用此設定並強制密碼重新整理，請在 SQL Server 組態管理員中開啟 Launchpad 服務的 [屬性] 窗格，按一下 [進階]，然後將 [重設外部使用者密碼] 變更為 [是]。 當您套用此變更時，系統會立即針對所有使用者帳戶重新產生密碼。 若要在此變更之後使用 R 指令碼，您必須重新啟動 Launchpad 服務，它就會讀取新產生的密碼。

若要定期重設密碼，您可以手動設定此旗標，或使用指令碼。

## <a name="see-also"></a>另請參閱

[擴充性架構](../concepts/extensibility-framework.md)

[安全性概觀](../concepts/security.md)
