---
title: Launchpad 帳戶設定
description: 如何修改在 SQL Server 上用來執行外部指令碼的 SQL Server Launchpad 服務帳戶。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1f05181e1a3069ec56f079751e43bd739424ce92
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "73727371"
---
# <a name="sql-server-launchpad-service-configuration"></a>SQL Server Launchpad 服務設定
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 是新服務，可管理和執行外部指令碼，就如同全文索引及查詢服務啟動個別的主機來處理全文查詢。

如需詳細資訊，請參閱 [SQL Server 機器學習服務的擴充性結構](../../advanced-analytics/concepts/extensibility-framework.md#launchpad)和 [SQL Server 機器學習服務中擴充性架構的安全性概觀](../../advanced-analytics/concepts/security.md#launchpad)中的 Launchpad 章節。

## <a name="account-permissions"></a>帳戶權限

根據預設，SQL Server Launchpad 會設定為在 **NT Service\MSSQLLaunchpad** 下執行，此帳戶已佈建用來執行外部指令碼的所有必要權限。 從這個帳戶移除權限可能會導致 Launchpad 無法啟動或存取應執行外部指令碼的 SQL Server 執行個體。

如果您修改服務帳戶，請務必使用[本機安全性原則主控台](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/how-to-configure-security-policy-settings)。

下表列出此帳戶所需的權限。

| 群組原則設定 | 固定名稱 |
|----------------------|---------------|
| [調整處理序的記憶體配額](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/adjust-memory-quotas-for-a-process) | SeIncreaseQuotaPrivilege | 
| [略過周遊檢查](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/bypass-traverse-checking) | SeChangeNotifyPrivilege | 
| [登入為服務](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/log-on-as-a-service) | SeServiceLogonRight | 
| [取代處理序層級權杖](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/replace-a-process-level-token) | SeAssignPrimaryTokenPrivilege | 

如需執行 SQL Server 服務所需權限的詳細資訊，請參閱[設定 Windows 服務帳戶與權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。

<a name="bkmk_ChangingConfig"></a> 

## <a name="configuration-properties"></a>設定屬性

一般而言，服務設定沒有理由需要修改。 可以變更的屬性包括服務帳戶、外部處理序計數 (預設為20 個)，或背景工作帳戶的密碼重設原則。

1. 開啟 [SQL Server 組態管理員](../../relational-databases/sql-server-configuration-manager.md)。

2. 在 [SQL Server 服務] 底下，以滑鼠右鍵按一下 [SQL Server Launchpad]，然後選取 [屬性]  。
  + 若要變更服務帳戶，請按一下 [登入]  索引標籤。
  + 若要增加使用者數目，請按一下 [進階]  索引標籤，然後變更 [資訊安全內容計數]  。

> [!Note]
> 在舊版的 SQL Server 2016 R Services 中，您可以藉由編輯 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 設定檔來變更服務的某些屬性。 此檔案不會再用來變更設定。 SQL Server 組態管理員是用來變更服務設定 (例如，服務帳戶和使用者數目) 的正確方法。

## <a name="debug-settings"></a>偵錯設定

有幾個屬性只能使用 Launchpad 的設定檔來加以變更，在偵錯之類的少數情況下，這可能很有用。 此設定檔會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝期間建立，並且預設會以純文字檔案儲存在 `<instance path>\binn\rlauncher.config`。

您必須在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的電腦上身為系統管理員，才能對此檔案進行變更。 如果您編輯了檔案，建議您在儲存變更前先備份副本。

下表會列出 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的進階設定，以及允許的值。

|**設定名稱**|**型別**|**說明**|
|----|----|----|
|JOB\_CLEANUP\_ON\_EXIT|整數 |這只是內部設定，請勿變更此值。 </br></br>指定為每個外部執行階段工作建立的暫存工作資料夾，是否應該在該工作階段完成後清理乾淨。 這項設定在偵錯時很有用。 </br></br>支援的值為 **0** (停用) 或 **1** (啟用)。 </br></br>預設值為 1，表示會在結束時移除記錄檔。|
|TRACE\_LEVEL|整數 |設定 MSSQLLAUNCHPAD 的追蹤詳細資訊層級以進行偵錯。 這會影響 LOG_DIRECTORY 設定所指定路徑中的追蹤檔案。 </br></br>支援的值為：**1** (錯誤)、**2** (效能)、**3** (警告)、**4** (資訊)。 </br></br>預設值為 1，表示只輸出錯誤。|

所有設定都會採用機碼值組的格式，分別位於獨立的行。 例如，若要變更追蹤層級，您可以新增這行：`Default: TRACE_LEVEL=4`。

<a name="bkmk_EnforcePolicy"></a>

## <a name="enforcing-password-policy"></a>強制執行密碼原則

如果您的組織要求定期變更密碼，您可能需要強制 Launchpad 服務重新產生為其工作者帳戶維護的加密密碼。

若要啟用此設定並強制密碼重新整理，請在 SQL Server 組態管理員中開啟 Launchpad 服務的 [屬性]  窗格，按一下 [進階]  ，然後將 [重設外部使用者密碼]  變更為 [是]  。 當您套用此變更時，系統會立即針對所有使用者帳戶重新產生密碼。 若要在此變更之後執行外部指令碼，您必須重新啟動 Launchpad 服務，它就會讀取新產生的密碼。

若要定期重設密碼，您可以手動設定此旗標，或使用指令碼。

## <a name="next-steps"></a>後續步驟

+ [擴充性架構](../concepts/extensibility-framework.md)
+ [安全性概觀](../concepts/security.md)
