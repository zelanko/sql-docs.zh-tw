---
title: 新增角色指派：編輯角色指派頁面 （報表管理員） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 3319ced0-4b86-42af-b18d-da41a625113c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fc4dd805faffb9fcf172f372f48d497a037fd16c
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59950154"
---
# <a name="new-role-assignment-edit-role-assignment-page-report-manager"></a>新增角色指派：編輯角色指派頁面 （報表管理員）
  您可以使用 [新增角色指派] 或 [編輯角色指派] 頁面來授與報表伺服器項目和作業的權限。 每位需要存取報表伺服器的使用者至少都必須具有一個定義存取層級的角色指派。 您可以在根節點，或在特定的報表、模型、資料夾、資源或共用資料來源上，建立角色指派。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 透過您套用至項目的角色指派，可以強制執行安全性。 角色指派使群組或使用者符合角色定義，其中每一個角色定義識別群組或使用者可對特定項目執行的工作。  
  
 項目層級角色指派可能影響的層面很廣。 雖然它們可與單一報表或資料夾產生關聯，但也可以定義於資料夾階層的高層級，而由樹狀目錄中較低層級的資料夾和項目來繼承。 如需這些預先定義角色的詳細資訊，請參閱 [將報表伺服器的存取權授與使用者 &#40;報表管理員&#41;](security/grant-user-access-to-a-report-server.md)。  
  
## <a name="navigation"></a>巡覽  
 您可以使用下列程序，在使用者介面 (UI) 中導覽至這個位置。  
  
###### <a name="to-open-the-new-role-assignment-or-edit-role-assignment-page"></a>若要開啟新增角色指派或編輯角色指派頁面  
  
1.  開啟報表管理員，然後找出您想要加入新角色指派或編輯角色指派的項目。  
  
2.  將滑鼠停留在該項目上，然後按一下下拉箭號。  
  
3.  在下拉式功能表中，按一下 **[安全性]**。 這樣就會開啟該項目的 [安全性] 屬性頁面。  
  
4.  如果您想要加入新的角色指派，請在工具列中，按一下 **[新增角色指派]**。 如果您想要編輯角色指派，請按一下想要編輯之群組或使用者名稱旁的 **[編輯]** 。  
  
    > [!NOTE]  
    >  如果某個項目目前是從父項目繼承安全性，請按一下工具列中的 **[編輯項目安全性]** 來變更安全性設定。  
  
## <a name="options"></a>選項。  
 **群組或使用者名稱**  
 輸入要建立其角色指派的群組或使用者帳戶的名稱。 群組或使用者名稱必須是有效的 Windows 網域帳戶。 這種格式來輸入帳戶：\<網域 >\\< 帳戶\>。  
  
> [!NOTE]  
>  這個方塊只有 [新增角色指派] 頁面才有提供。  
  
 **角色**  
 顯示報表伺服器中定義的全部角色，可用來定義項目的安全性。 在建立或變更報表或資料夾的角色指派時，請選取一或多個角色，直到結合的工作集描述使用者獲准執行的動作為止。 若要檢視每一個角色支援的工作集，請使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]。 您無法在報表管理員中檢視、建立、修改或刪除角色。 如需相關指示，請參閱 <<c0> [ 建立、 刪除或修改角色&#40;Management Studio&#41;](security/role-definitions-create-delete-or-modify.md)。</c0>  
  
 **說明**  
 顯示有關角色的其他資訊。 針對預先定義的角色，例如 **[瀏覽器]** 或 **[內容管理員]**，描述會摘要每個角色支援的工作。  
  
 **刪除角色指派**  
 按一下即可刪除使用者或群組的現有角色指派。 如果它是唯一留下的角色指派，就不可以刪除該角色指派 (每一個項目至少都必須具有一個角色指派)。  
  
> [!NOTE]  
>  這個按鈕只有 [編輯角色指派] 頁面才有提供。  
  
## <a name="see-also"></a>另請參閱  
 [建立、刪除或修改角色 &#40;Management Studio&#41;](security/role-definitions-create-delete-or-modify.md)   
 [在原生模式報表伺服器上授與權限](security/granting-permissions-on-a-native-mode-report-server.md)   
 [報表管理員 &#40;SSRS 原生模式&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [報表管理員 F1 說明](../../2014/reporting-services/report-manager-f1-help.md)   
 [角色指派](security/role-assignments.md)   
 [將報表伺服器的存取權授與使用者 &#40;報表管理員&#41;](security/grant-user-access-to-a-report-server.md)  
  
  
