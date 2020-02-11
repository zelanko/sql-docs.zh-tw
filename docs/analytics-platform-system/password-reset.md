---
title: 密碼重設
description: '[密碼重設] 頁面可讓您變更分析平臺系統所使用之系統管理員帳戶的密碼。'
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 952dbda04b4f7132406e3a6de4479afea1be92e7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "74400898"
---
# <a name="password-reset---analytics-platform-system"></a>密碼重設-Analytics Platform System
[**密碼重設**] 頁面可讓您變更分析平臺系統所使用之系統管理員帳戶的密碼。  
  
> [!WARNING]  
> 請一律使用**Configuration Manager**來更新設備網域系統管理員密碼。 其他方法可能不會更新分析平臺系統的所有元件，而且可能會導致設備存取問題。  
  
傳遞應用裝置時，您會獲得分析平臺系統密碼。 當您負責設備時，請一律將密碼變更為新的值。 有三個要更新的密碼。 密碼不一定要彼此相同。  
  
**F<*xxxx*> \administrator**  
設備網域的**系統管理員**。  
  
**.\Administrator**  
裝載虛擬機器之電腦上的本機**系統管理員**帳戶。  
  
> [!IMPORTANT]  
> 針對設備更新1， **Configuration Manager**不會適當地變更整個 PDW VM 的本機系統管理員帳戶密碼。 如果這是必要的，請聯絡 CSS 以取得其他指示。  
  
**sa**  
SQL Server 中的**sa**登入。 **sa**是**sysadmin**固定伺服器角色的成員，而且是 SQL Server 系統管理員。 您也可以使用**ALTER login**語句來變更**sa**登入的密碼。  
  
## <a name="password-requirements"></a>密碼需求  
網域系統管理員認證和系統管理員認證都會遵守每種認證類型的密碼強度原則。 變更網域系統管理員認證時，新的密碼會在 SQL Server PDW 時，將其更新為網域。  
  
> [!IMPORTANT]  
> SQL Server PDW 不支援網域系統管理員或本機系統**$** 管理員密碼中的貨幣符號字元（）。 密碼中允許使用 **^% &** 字元，不過，PowerShell 會將其視為特殊字元。 如果系統管理員的密碼或 SQL Server**sa**帳戶（安裝期間的**AdminPassword**和**PdwSAPassword**參數）使用其中任何字元，則安裝程式（包括安裝、升級、REPLACENODE 和修補）將會失敗。 為確保當目前的密碼包含不支援的字元時成功升級，請在執行升級之前，變更這些密碼，使其不包含這類字元。 升級完成之後，您可以將這些密碼設定回其原始值。 如需有關密碼需求的詳細資訊，請參閱[ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md)。  
  
## <a name="to-reset-a-password"></a>重設密碼  
  
1.  連接到控制節點，並啟動**Configuration Manager** （**dwconfig**）。 如需詳細資訊，請參閱[&#40;分析平臺系統&#41;啟動 Configuration Manager ](launch-the-configuration-manager.md)。  
  
2.  在**Configuration Manager**的左窗格中，按一下 [**密碼重設**]。  
  
3.  從 [**帳戶**] 下拉式功能表中選取 [系統管理員] 類型，然後在 [**密碼**] 和 [**確認密碼**] 方塊中輸入新的密碼。 按一下 **[** 套用] 以儲存變更。  
  
    您對這些帳戶所做的變更不會影響任何目前作用中的會話，但會在每個使用者下次嘗試登入時套用。  
  
    ![SQL Server DWConfig 密碼](./media/password-reset/SQL_Server_PDW_DWConfig_TopPW.png "SQL_Server_PDW_DWConfig_TopPW")  
  
## <a name="see-also"></a>另請參閱  
[設定系統管理員密碼以登入目錄服務還原模式中的 AD 節點 &#40;DSRM&#41; &#40;分析平臺系統&#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md)  
[啟動 Configuration Manager &#40;分析平臺系統&#41;](launch-the-configuration-manager.md)  
  
