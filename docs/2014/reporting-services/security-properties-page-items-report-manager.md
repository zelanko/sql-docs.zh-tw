---
title: 安全性屬性頁面，項目 （報表管理員） |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 351b8503-354f-4b1b-a7ac-f1245d978da0
caps.latest.revision: 27
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: c072df6e055cbf0bc0fc0dc503b6dfd55a4c8a29
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030714"
---
# <a name="security-properties-page-items-report-manager"></a>安全性屬性頁面，項目 (報表管理員)
  使用安全性屬性頁面來檢視或修改安全性設定，以決定資料夾、報表、模型、資源和共用資料來源的存取權。 此頁面適用於您有權保護的項目。  
  
 透過指定群組或使用者可執行的工作的角色指派來定義項目的存取權。 角色指派含有一個使用者或群組名稱，以及一個或多個指定工作集合的角色定義。  
  
 安全性設定是由根資料夾繼承至子資料夾和那些資料夾內的項目。 除非您明確地中斷繼承的安全性，否則子資料夾和項目會繼承父項目的安全性內容。 如果您為階層中間的資料夾重新定義安全性原則，所有其子項目 (包括子資料夾) 都會採用新的安全性設定。  
  
## <a name="navigation"></a>導覽  
 您可以使用下列程序，在使用者介面 (UI) 中導覽至這個位置。  
  
###### <a name="to-open-the-security-page-for-an-item"></a>若要開啟項目的安全性頁面  
  
1.  開啟報表管理員，然後找出您想要設定安全性設定的項目。  
  
2.  將滑鼠停留在該項目上，然後按一下下拉箭號。  
  
3.  在下拉式功能表中，執行下列其中一項步驟：  
  
    -   按一下 **[安全性]**。 這樣就會開啟該項目的 [安全性] 屬性頁面。  
  
    -   按一下 **[管理]** 開啟項目的 [一般] 屬性頁面。 然後，選取 **[安全性]** 索引標籤。  
  
 **編輯項目安全性**  
 按一下即可變更定義目前項目安全性的方式。 如果您編輯資料夾的安全性，您的變更將套用至目前資料夾及其任何子資料夾的內容。  
  
 [首頁] 資料夾不可使用此按鈕。  
  
 編輯項目安全性時，可以使用下列按鈕。  
  
 **刪除**  
 選取您要刪除的群組或使用者名稱旁的核取方塊，然後按一下 **[刪除]**。 如果它是留下的唯一角色指派，或是定義報表伺服器之安全性基準的內建角色指派 (例如，「Built-in\Administrators」)，則無法將其刪除。 刪除角色指派不會刪除群組或使用者帳戶或角色定義。  
  
 **新增角色指派**  
 按一下即可開啟 [新增角色指派] 頁面，可用來建立目前項目的其他角色指派。 如需詳細資訊，請參閱[新增角色指派： 編輯角色指派頁面&#40;報表管理員&#41;](../../2014/reporting-services/new-role-assignment-edit-role-assignment-page-report-manager.md)。  
  
 **還原為父安全性**  
 按一下即可將安全性設定重設為直屬父資料夾的安全性設定。 如果報表伺服器資料夾階層中都未打破繼承，則使用最上層資料夾 [首頁] 的安全性設定。  
  
 **群組或使用者**  
 列出屬於目前項目的現有角色指派之一部份的群組和使用者。 目前資料夾的現有角色指派是為此資料行中顯示的群組和使用者所定義的。 您可以按一下群組或使用者名稱以檢視或編輯角色指派詳細資料。  
  
 **角色**  
 列出屬於現有角色指派一部分的一個或多個角色定義。 如果有多個角色指派至群組或使用者帳戶，則該群組或使用者可以執行屬於該角色的所有工作。 若要檢視與某個角色相關聯的工作，請使用 SQL Server Management Studio 來檢視每個角色定義中的工作。  
  
## <a name="see-also"></a>另請參閱  
 [報表管理員 F1 說明](../../2014/reporting-services/report-manager-f1-help.md)   
 [預先定義的角色](security/role-definitions-predefined-roles.md)   
 [在原生模式報表伺服器上授與權限](security/granting-permissions-on-a-native-mode-report-server.md)   
 [角色指派](security/role-assignments.md)   
 [角色定義](security/role-definitions.md)  
  
  