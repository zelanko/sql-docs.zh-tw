---
title: 安全性頁面 (站台設定， 報表管理員） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: acc9a905-90f8-4544-aec6-b2ab3a1b0015
caps.latest.revision: 26
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: a613f3d2cadae9913f14759ca3c59252d62cd14f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37294098"
---
# <a name="security-page-site-settings-report-manager"></a>安全性頁面 (站台設定， 報表管理員)
  您可以使用 [安全性] 頁面來檢視控制報表伺服器站台之存取權的系統角色指派。 系統角色指派存在報表伺服器命名空間或資料夾階層的範圍之外。 系統角色指派是全域的，不會因特定項目而改變。 透過系統角色指派支援的作業包括建立和使用共用排程、使用報表產生器，以及設定某些伺服器功能的預設值。  
  
 安裝報表伺服器時，會建立預設的系統角色指派。 此系統角色指派會授與本機系統管理員權限，以管理報表伺服器環境。 本機系統管理員永遠可以設定本機報表伺服器的安全性，即使刪除系統角色指派也一樣。  
  
 需要存取報表產生器或共用排程的所有其他使用者都必須被指派至系統角色指派。  
  
## <a name="navigation"></a>導覽  
 您可以使用下列程序，在使用者介面 (UI) 中導覽至這個位置。  
  
###### <a name="to-open-the-security-page-for-site-settings"></a>若要開啟站台設定的安全性頁面  
  
1.  開啟報表管理員。  
  
2.  在頁面的頂端，按一下 **[站台設定]**。 這樣就會開啟該站台的 [一般] 屬性頁面。  
  
3.  選取 **[安全性]** 索引標籤。  
  
## <a name="options"></a>選項。  
 **刪除**  
 按一下即可刪除現有的角色指派。 在按一下 **[刪除]** 之前，請選取您要移除之群組或使用者名稱旁邊的核取方塊。 如果某個角色指派是唯一剩餘的角色指派，您就無法刪除它。 刪除角色指派不會刪除群組或使用者帳戶或角色定義。  
  
 **新增角色指派**  
 按一下即可開啟 [新增系統角色指派] 頁面，可用來建立報表伺服器站台的其他系統角色指派。 如需詳細資訊，請參閱 <<c0> [ 新增系統角色指派： 編輯系統角色指派頁面&#40;報表管理員&#41;](../../2014/reporting-services/new-system-role-assignments-edit-system-role-assignments-page-report-manager.md)。</c0>  
  
 **編輯**  
 按一下即可開啟 [編輯系統角色指派] 頁面，可用來編輯報表伺服器站台的個別系統角色指派。 如需詳細資訊，請參閱 <<c0> [ 新增系統角色指派： 編輯系統角色指派頁面&#40;報表管理員&#41;](../../2014/reporting-services/new-system-role-assignments-edit-system-role-assignments-page-report-manager.md)。</c0>  
  
 **群組或使用者**  
 列出屬於現有角色指派之一部份的群組和使用者。 目前資料夾的現有角色指派是為此資料行中顯示的群組和使用者所定義的。 按一下群組或使用者名稱旁的 **[編輯]** ，即可檢視或編輯角色指派詳細資料。  
  
 **角色**  
 列出屬於現有角色指派一部分的一個或多個角色定義。 如果有多個角色指派至群組或使用者帳戶，則該群組或使用者可以執行屬於所有角色的所有工作。 若要檢視的每一個角色支援的工作集，請使用[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]。 您無法在報表管理員中檢視、建立、修改或刪除角色。 如需相關指示，請參閱 <<c0> [ 建立、 刪除或修改角色&#40;Management Studio&#41;](security/role-definitions-create-delete-or-modify.md)。</c0>  
  
## <a name="see-also"></a>另請參閱  
 [報表管理員 F1 說明](../../2014/reporting-services/report-manager-f1-help.md)   
 [在原生模式報表伺服器上授與權限](security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
