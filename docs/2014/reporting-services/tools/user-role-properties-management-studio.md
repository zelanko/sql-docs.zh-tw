---
title: 使用者角色屬性 (Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.userroleproperties.f1
ms.assetid: c8b22236-a8b1-4e15-b1ff-4e1909b602d3
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: bb8c7b6467b862d13f242debf0d963012b44bb61
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56015484"
---
# <a name="user-role-properties-management-studio"></a>使用者角色屬性 (Management Studio)
  您可以使用這個頁面來檢視項目層級角色定義中包含的工作。 您也可以使用這個頁面來變更工作清單或修改角色描述。  
  
 項目層級角色定義是指使用者針對特定項目 (亦即，資料夾、報表或資源或共用資料來源) 所執行之工作的具名集合。 角色定義會指派給使用者或群組，以便在報表管理員中建立角色指派。 角色定義中的工作會描述使用者或群組可執行的工作。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 包含許多您可以使用之預先定義的項目層級角色定義。 您可以透過變更每個角色定義的工作清單，修改角色定義。 編輯角色定義將影響包含該角色定義的所有角色指派。  
  
> [!NOTE]  
>  使用者角色指派只會用於以原生模式執行的報表伺服器。 如果報表伺服器是針對 SharePoint 整合所設定，這個頁面就會顯示有關 SharePoint 網站上所定義之角色和權限等級的唯讀資訊。  
  
## <a name="options"></a>選項。  
 **名稱**  
 指定角色定義的名稱。  
  
 **說明**  
 顯示角色定義的描述。 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，這項描述只會出現在本頁面上。 在報表管理員中，這項描述可協助使用者決定是否要在角色指派中使用角色。  
  
 **工作**  
 列出可為此角色定義選取的所有項目層級工作。 您可以將項目加入預先定義的工作清單，或者從清單移除項目，以定義使用者藉由這個角色存取指定項目的方式。 您不能建立新的工作，也不能修改現有的工作。 角色定義的工作清單只會顯示在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中。  
  
 **工作描述**  
 提供每個工作的相關資訊。 您不能修改工作描述。  
  
## <a name="see-also"></a>另請參閱  
 [項目層級工作](../security/tasks-and-permissions-item-level-tasks.md)   
 [角色定義](../security/role-definitions.md)   
 [Management Studio F1 說明中的報表伺服器](report-server-in-management-studio-f1-help.md)   
 [工作和權限](../security/tasks-and-permissions.md)   
 [預先定義的角色](../security/role-definitions-predefined-roles.md)  
  
  
