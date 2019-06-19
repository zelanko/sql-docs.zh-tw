---
title: 角色指派 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- users [Reporting Services]
- roles [Reporting Services]
- role-based security [Reporting Services], role assignments
- groups [Reporting Services]
- security [Reporting Services], role assignments
ms.assetid: 600e112c-1897-48a6-93c0-6e9f3f12dc01
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 556abc4ff00df4393c756f62072254e417653f40
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66101870"
---
# <a name="role-assignments"></a>角色指派
  在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中，「角色指派」  會決定預存項目以及報表伺服器本身的存取權。 角色指派包含下列部份：  
  
-   您想要控制存取權的安全性實體項目。 安全性實體項目的範例包括資料夾、報表和資源。  
  
-   可以利用 Windows 安全性，或其他驗證機制驗證的使用者或群組帳戶。  
  
-   定義一組工作的角色定義。 角色定義的範例包括 **系統管理員**、 **內容管理員**和 **發行者**。  
  
 角色指派會在資料夾階層中繼承。 資料夾中包含的所有報表、共用資料來源、資源以及子資料夾，會自動繼承針對該資料夾定義的角色指派。 您可以為個別項目定義角色指派，以覆寫繼承的安全性。 至少要有一個角色指派，以保護資料夾階層中所有的部份。 您不能建立非安全項目，或者以產生非安全項目的方式來操作設定。  
  
 下圖描述將一個群組和一個特定使用者對應至資料夾 B 之 **發行者** 角色的角色指派。  
  
 ![角色指派圖表](../media/report-securityarch.gif "角色指派圖表")  
角色指派圖表  
  
## <a name="system-level-and-item-level-role-assignments"></a>系統層級與項目層級角色指派  
 在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中以角色為基礎的安全性會組織成下列層級：  
  
-   項目層級角色指派會控制報表伺服器資料夾階層中之報表、資料夾、報表模型、共用資料來源以及資源的存取權。 在特定項目或 [主資料夾] 資料夾上建立角色指派時，會定義項目層級角色指派。  
  
-   系統角色指派會授權範圍遍及整個伺服器的作業 (例如，管理作業的能力就是系統層級作業)。 系統角色指派不等於系統管理員。 它並未授與完全控制報表伺服器的進階權限。  
  
 系統角色指派不會授權資料夾階層中之項目的存取權。 系統與項目安全性互斥。 針對任何給定使用者或群組，您可能需要建立系統層級與項目層級角色指派，以提供足夠的存取權給報表伺服器。  
  
## <a name="users-and-groups-in-role-assignments"></a>角色指派中的使用者與群組  
 您在角色指派中指定的使用者或群組帳戶屬於網域帳戶。 報表伺服器會從 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 網域 (如果您是使用自訂安全性延伸模組，則為另一個安全性模型) 參考 (但不會建立或管理) 使用者與群組。  
  
 在套用至任何給定項目的所有角色指派中，不會有兩個可以指定相同使用者或群組。 如果使用者帳戶也是群組帳戶的成員，而二者皆有角色指派，則兩個角色指派結合的工作皆可供使用者使用。  
  
 您將使用者加入至已經是角色指派之一部份的群組時，必須重設 Internet Information Services (IIS)，該使用者的新角色指派才會生效。  
  
## <a name="predefined-role-assignments"></a>預先定義的角色指派  
 依預設，會實作預先定義的角色指派，讓本機管理員可以管理報表伺服器。 您必須加入其他角色指派，將存取權授與其他使用者。  
  
 如需提供預設安全性之預先定義角色指派的詳細資訊，請參閱 [預先定義的角色](role-definitions-predefined-roles.md)。  
  
## <a name="see-also"></a>另請參閱  
 [建立、刪除或修改角色 &#40;Management Studio&#41;](role-definitions-create-delete-or-modify.md)   
 [將報表伺服器的存取權授與使用者 &#40;報表管理員&#41;](grant-user-access-to-a-report-server.md)   
 [修改或刪除角色指派 &#40;報表管理員&#41;](role-assignments-modify-or-delete.md)   
 [設定 SharePoint 網站上報表伺服器項目的權限 &#40;SharePoint 整合模式的 Reporting Services&#41;](set-permissions-for-report-server-items-on-a-sharepoint-site.md)   
 [在原生模式報表伺服器上授與權限](granting-permissions-on-a-native-mode-report-server.md)  
  
  
