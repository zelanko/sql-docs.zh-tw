---
title: 密碼重設
description: '[密碼重設] 頁面可讓您變更 Analytics Platform System 所用系統管理員帳戶的密碼。'
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 952dbda04b4f7132406e3a6de4479afea1be92e7
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400898"
---
# <a name="password-reset---analytics-platform-system"></a>密碼重設-Analytics Platform System
[ **密碼重設** ] 頁面可讓您變更 Analytics Platform System 所用系統管理員帳戶的密碼。  
  
> [!WARNING]  
> 請一律使用 **Configuration Manager** 來更新設備網域系統管理員密碼。 其他方法可能不會更新 Analytics Platform System 的所有元件，而且可能會導致設備存取問題。  
  
當設備傳遞時，系統會提供您分析平臺系統密碼給您。 當您負責設備時，請一律將密碼變更為新的值。 有三個要更新的密碼。 密碼不需要彼此相同。  
  
**F<*xxxx*> \administrator**  
設備網域的 **系統管理員** 。  
  
**.\Administrator**  
裝載虛擬機器之電腦上的本機 **系統管理員** 帳戶。  
  
> [!IMPORTANT]  
> 針對設備更新1， **Configuration Manager** 不會正確地變更整個 PDW VM 的本機系統管理員帳戶密碼。 如果這是必要的，請聯繫 CSS 以取得其他指示。  
  
**Sa**  
SQL Server 中的 **sa** 登入。 **sa** 是系統管理員（ **sysadmin** ）固定伺服器角色的成員，而且是 SQL Server 系統管理員。 您也可以使用**ALTER login**語句來變更**sa**登入的密碼。  
  
## <a name="password-requirements"></a>密碼需求  
網域系統管理員認證和系統管理員認證都遵循每一種認證類型的密碼強度原則。 變更網域系統管理員認證時，新密碼會在 SQL Server PDW 時，更新至網域。  
  
> [!IMPORTANT]  
> SQL Server PDW 不支援 **$** 網域系統管理員或本機系統管理員密碼中的貨幣符號字元 () 。 密碼中允許使用 **^% &** 字元，但 PowerShell 將這些字元視為特殊字元。 如果系統管理員或 SQL Server**sa** 帳戶的密碼中使用這些字元，則在安裝期間 (**AdminPassword** 和 **PdwSAPassword** 參數) 然後安裝程式（包括安裝、升級、REPLACENODE 和修補）將會失敗。 若要在目前的密碼包含不支援的字元時確保升級成功，請變更這些密碼，使其不包含這類字元，然後再執行升級。 升級完成之後，您可以將這些密碼重設回其原始值。 如需密碼需求的詳細資訊，請參閱 [ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md)。  
  
## <a name="to-reset-a-password"></a>重設密碼  
  
1.  連接到控制節點，並啟動 **Configuration Manager** (**dwconfig.exe**) 。 如需詳細資訊，請參閱 [啟動 Configuration Manager &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)。  
  
2.  在 **Configuration Manager**的左窗格中，按一下 [ **密碼重設**]。  
  
3.  從 [ **帳戶** ] 下拉式功能表中選取系統管理員類型，然後在 [ **密碼** ] 和 [ **確認密碼** ] 方塊中輸入新密碼。 按一下 [套用] 以儲存 **您的變更** 。  
  
    您對這些帳戶所做的變更不會影響任何目前作用中的會話，但會在每個使用者下次嘗試登入時套用。  
  
    ![SQL Server DWConfig 密碼](./media/password-reset/SQL_Server_PDW_DWConfig_TopPW.png "SQL_Server_PDW_DWConfig_TopPW")  
  
## <a name="see-also"></a>另請參閱  
[設定用來登入目錄服務還原模式 AD 節點的系統管理員密碼 &#40;DSRM&#41; &#40;Analytics Platform System&#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md)  
[啟動 Configuration Manager &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)  
  
