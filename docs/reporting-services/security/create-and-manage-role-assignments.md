---
title: 建立及管理角色指派 | Microsoft Docs
ms.date: 05/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- removing role assignments
- roles [Reporting Services], assignments
- security [Reporting Services], role assignments
- modifying role assignments
- deleting role assignments
ms.assetid: 086d0987-b43c-4834-8372-e08fb4b432f8
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 863904e2d82fc97045305dd2430241a91e333f11
ms.sourcegitcommit: 553ecea0427e4d2118ea1ee810f4a73275b40741
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 05/14/2019
ms.locfileid: "65619598"
---
# <a name="create-and-manage-role-assignments"></a>建立和管理角色指派

*角色指派*是一種安全性原則，可決定使用者或群組的權限。 權限可決定使用者或群組是否可存取或修改特定報表伺服器項目，或進行工作。 角色指派是由單一使用者或群組帳戶名稱以及一或多個角色定義所組成。

角色指派的範圍設定為 *「項目層級」* 或 *「系統層級」*。

- 項目層級角色指派是在特定項目或在報表伺服器上資料夾階層的分支中建立的。 導覽至特定資料夾或項目，即可為其建立角色指派。

- 系統層級角色指派會提供所選使用者能夠執行可影響整體報表伺服器站台之工作的功能。 這些工作包括：
  - 建立共用排程
  - 管理作業
  - 處理報表
  - 設定屬性

系統層級安全性不會傳遞報表伺服器資料夾階層中項目的存取權。

## <a name="creating-an-item-level-role-assignment"></a>建立項目層級角色指派

從這裡開始，您可以針對需要存取報表伺服器的每一個使用者或群組帳戶建立個別的角色指派。 如果帳戶不是在包含報表伺服器的網域上，請包括網域名稱。 指定帳戶之後，您可以選擇一或多個角色定義。 角色定義會是累加的。 特定使用者或群組的指派中，支援所有定義中結合的所有工作集。

若要啟用普遍存取權，您可以在資料夾階層中選擇較高的項目 (例如，主資料夾的根資料夾)。 稍後，您可以建立角色指派，以鎖定資料夾階層的特定區域。

您必須是報表伺服器電腦上本機系統管理員群組的成員，才能建立角色指派。 您可以將其他使用者指派給 **「內容管理員」** 角色來委派該項責任。

若要建立或管理角色指派，或需要詳細資訊，請參閱[將報表伺服器的存取權授與使用者](../../reporting-services/security/grant-user-access-to-a-report-server.md)
  
## <a name="creating-a-system-level-role-assignment"></a>建立系統層級角色指派

系統層級與項目層級角色指派會一起使用。 您可針對具有項目層級角色指派的每一個使用者或群組建立系統層級角色指派。

系統層級角色指派包括各種不同的權限，但是不包括屬於項目層級角色指派一部分的權限。

報表伺服器中的系統角色並不會傳遞包含所有可能工作的中心權限，與電腦上的系統權限相反。 系統層級角色指派只是以報表伺服器站台為範圍的一組工作。 系統角色指派會決定使用者是否可以檢視應用程式屬性 (例如首頁的影像或標題)、檢視或管理共用排程或是使用報表產生器。

若要建立或管理系統層級的角色指派，或需要詳細資訊，請參閱[將報表伺服器的存取權授與使用者](../../reporting-services/security/grant-user-access-to-a-report-server.md)和[預先定義角色](../../reporting-services/security/role-definitions-predefined-roles.md)。  

## <a name="modifying-a-role-assignment"></a>修改角色指派

您可以在任何時候修改角色指派。 所做的變更會在儲存角色指派時生效。 使用者工作階段不受角色指派變更的影響。 如果使用者已開啟報表，而且您將角色指派修改成拒絕存取，則使用者可以繼續使用該作用中工作階段的報表。

如果您將使用者帳戶加入至已經屬於某個角色指派的群組，則要經過一段延遲後，使用者帳戶才能從變更存取項目。 此延遲是 Internet Information Services (IIS) 快取驗證 Token 所造成的。 您可以等候 Token 重新整理 (通常是 15 分鐘)，或者可以重設 IIS 來立即更新快取。

您一次僅能修改一個角色指派。 您無法執行全域搜尋與取代作業來變更角色定義名稱或角色指派設定，或者尋找包括特定使用者或群組的所有角色指派。

## <a name="deleting-a-role-assignment"></a>刪除角色指派

您可以選取要刪除之每個指派旁的核取方塊，然後按一下 **[刪除]**，以刪除角色指派。 也可以按一下 **[還原為父安全性]**，以刪除角色指派。 當您選取此按鈕時，項目的現有角色指派會遭到刪除，並取代為繼承自父項目的指派。

## <a name="see-also"></a>另請參閱

[將報表伺服器的存取權授與使用者](../../reporting-services/security/grant-user-access-to-a-report-server.md)  
[角色指派](../../reporting-services/security/role-assignments.md)  
[角色定義](../../reporting-services/security/role-definitions.md)  
[預先定義的角色](../../reporting-services/security/role-definitions-predefined-roles.md)  
[在原生模式報表伺服器上授與權限](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)
