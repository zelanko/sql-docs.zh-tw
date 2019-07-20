---
title: SQL Server Launchpad 服務帳戶設定
description: 如何修改在 SQL Server 上用來執行外部腳本的 SQL Server Launchpad 服務帳戶。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 9146020fb35d729575c8441e71b711e287399a75
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345524"
---
# <a name="sql-server-launchpad-service-configuration"></a>SQL Server Launchpad 服務設定
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]是管理和執行外部腳本的服務, 類似于全文檢索索引和查詢服務啟動個別主控制項來處理全文檢索查詢的方式。

如需詳細資訊, 請參閱[SQL Server Machine Learning Services](../../advanced-analytics/concepts/security.md#launchpad)中擴充性架構的[SQL Server Machine Learning 服務](../../advanced-analytics/concepts/extensibility-framework.md#launchpad)和安全性總覽中的擴充性架構中的 [啟動列] 區段。

## <a name="account-permissions"></a>帳戶權限

根據預設, SQL Server Launchpad 設定為在**NT Service\MSSQLLaunchpad**下執行, 這會以所有必要的許可權布建, 以執行外部腳本。 從這個帳戶移除許可權可能會導致啟動列失敗, 或存取應執行外部腳本的 SQL Server 實例。

如果您修改服務帳戶, 請務必使用 [[本機安全性原則] 主控台](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/how-to-configure-security-policy-settings)。

下表列出此帳戶所需的許可權。

| 群組原則設定 | 常數名稱 |
|----------------------|---------------|
| [調整進程的記憶體配額](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/adjust-memory-quotas-for-a-process) | SeIncreaseQuotaPrivilege | 
| [略過遍歷檢查](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/bypass-traverse-checking) | SeChangeNotifyPrivilege | 
| [以服務方式登入](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/log-on-as-a-service) | SeServiceLogonRight | 
| [取代進程層級 token](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/replace-a-process-level-token) | SeAssignPrimaryTokenPrivilege | 

如需執行 SQL Server 服務所需權限的詳細資訊，請參閱[設定 Windows 服務帳戶與權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。

<a name="bkmk_ChangingConfig"></a> 

## <a name="configuration-properties"></a>設定屬性

一般而言, 不需要修改服務設定。 可以變更的屬性包括服務帳戶、外部進程的計數 (預設為 20), 或背景工作帳戶的密碼重設原則。

1. 開啟 [SQL Server 組態管理員](../../relational-databases/sql-server-configuration-manager.md)。

2. 在 [SQL Server 服務] 底下, 以滑鼠右鍵按一下 SQL Server Launchpad, 然後選取 [**屬性**]。
  + 若要變更服務帳戶, 請按一下 [**登**入] 索引標籤。
  + 若要增加使用者數目, 請按一下 [ **Advanced** ] 索引標籤, 然後變更 [**安全性內容計數**]。

> [!Note]
> 在舊版的 SQL Server 2016 R Services 中, 您可以藉由編輯[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]設定檔來變更服務的某些屬性。 此檔案不再用於變更設定。 SQL Server 組態管理員是服務設定變更的正確方法, 例如服務帳戶和使用者數目。

## <a name="debug-settings"></a>Debug 設定

只有幾個屬性只能使用啟動列的設定檔來變更, 這在有限的情況下可能很有用, 例如, 偵錯工具。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]設定期間會建立設定檔, 而且預設會以純文字檔案的形式儲存在中`<instance path>\binn\rlauncher.config`。

您必須在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的電腦上身為系統管理員，才能對此檔案進行變更。 如果您編輯了檔案，建議您在儲存變更前先備份副本。

下表列出的 advanced 設定[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], 以及允許的值。

|**設定名稱**|**型別**|**描述**|
|----|----|----|
|結束時\_ \_清除\_作業|Integer |這是僅供內部設定-請勿變更此值。 </br></br>指定是否應該在會話完成後清除為每個外部執行時間會話建立的暫存工作資料夾。 這項設定在偵錯時很有用。 </br></br>支援的值為**0** (已停用) 或**1** (已啟用)。 </br></br>預設值為 1, 表示記錄檔會在結束時移除。|
|追蹤\_層級|Integer |設定 MSSQLLAUNCHPAD 的追蹤詳細資訊層級, 以進行偵錯工具。 這會影響 LOG_DIRECTORY 設定所指定之路徑中的追蹤檔案。 </br></br>支援的值為：**1** (錯誤)、 **2** (效能)、 **3** (警告)、 **4** (資訊)。 </br></br>預設值為 1, 表示只輸出錯誤。|

所有設定都會採用機碼值組的格式，分別位於獨立的行。 例如, 若要變更追蹤層級, 您可以加入這一行`Default: TRACE_LEVEL=4`。

<a name="bkmk_EnforcePolicy"></a>

## <a name="enforcing-password-policy"></a>強制執行密碼原則

如果您的組織要求定期變更密碼，您可能需要強制 Launchpad 服務重新產生為其工作者帳戶維護的加密密碼。

若要啟用此設定並強制密碼重新整理，請在 SQL Server 組態管理員中開啟 Launchpad 服務的 [屬性]  窗格，按一下 [進階]  ，然後將 [重設外部使用者密碼]  變更為 [是]  。 當您套用此變更時，系統會立即針對所有使用者帳戶重新產生密碼。 若要在這次變更之後執行外部腳本, 您必須重新開機啟動列服務, 此時它會讀取新產生的密碼。

若要定期重設密碼，您可以手動設定此旗標，或使用指令碼。

## <a name="next-steps"></a>後續步驟

+ [擴充性架構](../concepts/extensibility-framework.md)
+ [安全性概觀](../concepts/security.md)
