---
title: 密碼重設-Analytics Platform System |Microsoft 文件
description: 重設密碼 頁面可讓您變更 Analytics Platform System 所用的系統管理員帳戶的密碼。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 63fbb097bf1ca926223ce7c0114c8da5d10cd969
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/19/2018
ms.locfileid: "31539418"
---
# <a name="password-reset---analytics-platform-system"></a>密碼重設-Analytics Platform System
**密碼重設**頁面可讓您變更 Analytics Platform System 所用的系統管理員帳戶的密碼。  
  
> [!WARNING]  
> 一律使用**Configuration Manager**更新應用裝置的網域系統管理員密碼。 其他方法可能會無法更新 Analytics Platform System 的所有元件，而且可能會造成應用裝置的存取問題。  
  
傳遞應用裝置時，您會獲得 Analytics Platform System 密碼。 當您要負責您的應用裝置，一律變更成新值的密碼。 有三個更新的密碼。 密碼不必與彼此相同。  
  
**F <*xxxx*> \Administrator**  
**管理員**的應用裝置的網域。  
  
**.\Administrator**  
本機**管理員**裝載虛擬機器的電腦上的帳戶。  
  
> [!IMPORTANT]  
> 應用裝置更新 1， **Configuration Manager**不會無法正確地變更整個 PDW VM 的本機系統管理員帳戶的密碼。 如果這是必要，請連絡 CSS，如需其他指示。  
  
**sa**  
**Sa** SQL Server 中的登入。 **sa**隸屬**sysadmin**固定伺服器角色和 SQL Server 系統管理員。 密碼**sa**登入也可以變更利用**ALTER LOGIN**陳述式。  
  
## <a name="password-requirements"></a>密碼的需求  
每種類型的認證的密碼強度原則符合網域系統管理員認證和系統管理員認證。 新的密碼變更時的網域系統管理員認證，會更新為網域所需整個 SQL Server PDW。  
  
> [!IMPORTANT]  
> SQL Server PDW 不支援貨幣符號字元 (**$**) 中的網域系統管理員或本機系統管理員密碼。 字元 **^ %&** 允許的密碼，但 PowerShell 目前這些特殊字元。 如果下列任何字元的密碼中使用的系統管理員或 SQL Server**sa**帳戶 ( **AdminPassword**和**PdwSAPassword**期間的參數安裝程式） 然後安裝程式，包括安裝、 升級、 REPLACENODE 和修補，將會失敗。 若要確保升級成功，當目前的密碼包含不支援的字元，變更這些密碼，使它們不包含這類字元執行升級之前。 升級完成之後，您可以設定這些密碼回其原始值。 如需密碼需求的詳細資訊，請參閱[ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md)。  
  
## <a name="to-reset-a-password"></a>重設密碼  
  
1.  連接到控制節點並啟動**Configuration Manager** (**dwconfig.exe**)。 如需詳細資訊，請參閱[啟動 Configuration Manager &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)。  
  
2.  在左窗格中**Configuration Manager**，按一下 **密碼重設**。  
  
3.  選取系統管理員類型，從**帳戶**下拉式選單，然後輸入中的新密碼**密碼**和**確認密碼**方塊。 按一下**套用**以儲存變更。  
  
    您對這些帳戶的變更不會影響任何目前作用中的工作階段，但將在下一次登入嘗試每個使用者套用。  
  
    ![SQL Server DWConfig 密碼](./media/password-reset/SQL_Server_PDW_DWConfig_TopPW.png "SQL_Server_PDW_DWConfig_TopPW")  
  
## <a name="see-also"></a>另請參閱  
[在目錄服務還原模式中設定系統管理員密碼來登入 AD 節點&#40;DSRM&#41; &#40;Analytics Platform System&#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md)  
[啟動 Configuration Manager &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)  
  
