---
title: 密碼重設-Analytics Platform System |Microsoft Docs
description: 密碼重設 頁面可讓您變更使用 Analytics Platform System 的系統管理員帳戶的密碼。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5fb3bbb5adba5754c220c34503a22656f6da39c5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960465"
---
# <a name="password-reset---analytics-platform-system"></a>密碼重設-Analytics Platform System
**密碼重設**頁面可讓您變更使用 Analytics Platform System 的系統管理員帳戶的密碼。  
  
> [!WARNING]  
> 一律使用**Configuration Manager**更新設備網域系統管理員密碼。 其他方法可能不會更新 Analytics Platform System 的所有元件，並可能會導致設備存取問題。  
  
設備傳遞時，您會獲得 Analytics Platform System 密碼。 當您要負責您的應用裝置時，一律變更成新值的密碼。 有三個更新的密碼。 密碼不必與彼此相同。  
  
**F <*xxxx*> \Administrator**  
**系統管理員**的設備網域。  
  
**.\Administrator**  
本機**系統管理員**裝載虛擬機器的電腦上的帳戶。  
  
> [!IMPORTANT]  
> 設備更新 1， **Configuration Manager**不會無法正確地變更整個 PDW VM 的本機系統管理員帳戶的密碼。 如果這是必要項目，請連絡 CSS，如需其他指示。  
  
**sa**  
**Sa** SQL Server 中的登入。 **sa**隸屬**sysadmin**固定伺服器角色和 SQL Server 系統管理員。 密碼**sa**登入也可以變更利用**ALTER LOGIN**陳述式。  
  
## <a name="password-requirements"></a>密碼的需求  
網域系統管理員認證和系統管理員認證遵守每種類型的認證的密碼強度原則。 新的密碼變更時的網域系統管理員認證，會更新網域在需要時在 SQL Server PDW。  
  
> [!IMPORTANT]  
> SQL Server PDW 不支援的貨幣符號字元 ( **$** ) 中的網域系統管理員或本機系統管理員密碼。 字元 **^ %&** 允許使用密碼，不過，PowerShell 會將這些特殊字元。 如果下列任何字元的密碼中使用的系統管理員或 SQL Server**sa**帳戶 ( **AdminPassword**並**PdwSAPassword**期間的參數安裝程式） 就設定，包括安裝、 升級、 REPLACENODE 和修補，將會失敗。 若要確保升級成功，目前的密碼包含不支援的字元時，請變更這些密碼，使它們不包含這類字元執行升級之前。 升級完成之後，您可以設定這些密碼回其原始值。 如需有關密碼需求的詳細資訊，請參閱[ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md)。  
  
## <a name="to-reset-a-password"></a>若要重設密碼  
  
1.  連接到控制節點並啟動**Configuration Manager** (**dwconfig.exe**)。 如需詳細資訊，請參閱 <<c0> [ 啟動組態管理員 &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)。</c0>  
  
2.  在左窗格中**Configuration Manager**，按一下**密碼重設**。  
  
3.  選取系統管理員類型，從**帳戶**下拉式選單，然後輸入中的新密碼**密碼**並**確認密碼**方塊。 按一下 **套用**以儲存變更。  
  
    您對這些帳戶的變更不會影響任何目前作用中的工作階段，但會套用在每個使用者下一步 的登入嘗試。  
  
    ![SQL Server DWConfig 密碼](./media/password-reset/SQL_Server_PDW_DWConfig_TopPW.png "SQL_Server_PDW_DWConfig_TopPW")  
  
## <a name="see-also"></a>另請參閱  
[在 目錄服務還原模式中設定登入 AD 節點的系統管理員密碼&#40;DSRM&#41; &#40;Analytics Platform System&#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md)  
[啟動組態管理員 &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)  
  
