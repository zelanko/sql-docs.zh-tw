---
title: 建立及管理角色指派 | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: security
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- removing role assignments
- roles [Reporting Services], assignments
- security [Reporting Services], role assignments
- modifying role assignments
- deleting role assignments
ms.assetid: 086d0987-b43c-4834-8372-e08fb4b432f8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4e0579c3d9d48ea9ac833829e571cf09b6c0dcd3
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2018
ms.locfileid: "43281464"
---
# <a name="create-and-manage-role-assignments"></a>建立和管理角色指派
  *「角色指派」* (Role assignment) 是一種安全性原則，可決定使用者或群組是否能夠存取特定的報表伺服器項目或執行作業。 角色指派是由單一使用者或群組帳戶名稱以及一或多個角色定義所組成。  
  
 角色指派的範圍設定為 *「項目層級」* 或 *「系統層級」*。  
  
-   項目層級角色指派永遠是建立在特定項目的內容中或報表伺服器資料夾階層的分支中。 導覽至特定資料夾或項目，即可為其建立角色指派。  
  
-   系統層級角色指派會提供選定使用者能夠執行可影響整體報表伺服器站台之工作的能力。 這些工作包括建立共用排程、管理作業、在報表產生器中處理報表，以及設定屬性。 系統層級安全性不會傳遞報表伺服器資料夾階層中項目的存取權。  
  
## <a name="creating-an-item-level-role-assignment"></a>建立項目層級角色指派  
 若要建立或管理角色指派，請使用報表管理員，並開啟您想要維護安全之項目的 [安全性] 屬性頁。  
  
 您必須針對需要存取報表伺服器的每一個使用者或群組帳戶建立個別的角色指派。 如果帳戶不是在包含報表伺服器的網域上，請包括網域名稱。 指定帳戶之後，您可以選擇一或多個角色定義。 角色定義會是累加的。 特定使用者或群組的指派中，支援所有定義中之結合的所有工作集。  
  
 若要啟用普遍存取權，您應該在資料夾階層中選擇較高的項目 (例如，根節點 [主資料夾])。 接著，您可以建立後續角色指派，以鎖定資料夾階層的特定區域。  
  
 您必須是報表伺服器電腦上本機系統管理員群組的成員，才能建立角色指派。 您可以將其他使用者指派給 **「內容管理員」** 角色來委派該項責任。  
  
 如需詳細資訊，請參閱 [將報表伺服器的存取權授與使用者 &#40;報表管理員&#41;](../../reporting-services/security/grant-user-access-to-a-report-server-report-manager.md)。  
  
## <a name="creating-a-system-level-role-assignment"></a>建立系統層級角色指派  
 若要建立或管理系統層級角色指派，請使用報表管理員，並開啟 [站台設定] 頁面。  
  
 系統層級與項目層級角色指派會一起使用。 您應該針對具有項目層級角色指派的每一個使用者或群組建立系統層級角色指派。  
  
 系統層級角色指派包括各種不同的權限，但是不包括屬於項目層級角色指派之一部分的權限。 報表伺服器中的系統角色並不會傳遞包含完整之所有可能作業集合的中心權限，與電腦上的系統權限相反。 系統層級角色指派只是以報表伺服器站台為範圍的一組工作。 透過系統角色指派所傳遞的權限會決定使用者是否可以檢視應用程式屬性 (例如首頁的影像或標題)、檢視或管理共用排程或是使用報表產生器。  
  
 如需詳細資訊，請參閱 [將報表伺服器的存取權授與使用者 &#40;報表管理員&#41;](../../reporting-services/security/grant-user-access-to-a-report-server-report-manager.md) 和 [預先定義的角色](../../reporting-services/security/role-definitions-predefined-roles.md)。  
  
## <a name="modifying-a-role-assignment"></a>修改角色指派  
 您可以在任何時候修改角色指派。 所做的變更會在儲存角色指派時生效。 使用者工作階段不受角色指派變更的影響。 如果使用者已開啟報表，而您將角色指派修改成拒絕存取，只要工作階段為使用中，使用者就可以繼續使用報表。  
  
 如果您將使用者帳戶加入至已經屬於某個角色指派的群組，則要經過一段延遲後，使用者帳戶才能透過群組帳戶原則存取項目。 此延遲是 Internet Information Services (IIS) 快取驗證 Token 所造成的。 您可以等候 Token 重新整理 (等候期間通常是 15 分鐘)，或者可以重設 IIS 來立即更新快取。  
  
 您一次僅能修改一個角色指派。 您無法執行全域搜尋與取代作業來變更角色定義名稱或角色指派設定，或者尋找所有包括特定使用者或群組的角色指派。  
  
## <a name="deleting-a-role-assignment"></a>刪除角色指派  
 您可以選取要刪除之每個指派旁的核取方塊，然後按一下 **[刪除]**，以刪除角色指派。 也可以按一下 **[還原為父安全性]**，以刪除角色指派。 當您按一下此按鈕時，會刪除項目的現有角色指派，並以父項目提供的角色指派來取代。  
  
## <a name="see-also"></a>另請參閱  
 [將報表伺服器的存取權授與使用者 &#40;報表管理員&#41;](../../reporting-services/security/grant-user-access-to-a-report-server-report-manager.md)   
 [修改或刪除角色指派 &#40;報表管理員&#41;](../../reporting-services/security/role-assignments-modify-or-delete.md)   
 [角色指派](../../reporting-services/security/role-assignments.md)   
 [角色定義](../../reporting-services/security/role-definitions.md)   
 [Predefined Roles](../../reporting-services/security/role-definitions-predefined-roles.md)   
 [在原生模式報表伺服器上授與權限](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
