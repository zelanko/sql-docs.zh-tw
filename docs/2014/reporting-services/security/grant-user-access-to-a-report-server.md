---
title: 授與使用者存取報表伺服器 （報表管理員） |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- removing role assignments
- permissions [Reporting Services], granting report server access
- roles [Reporting Services], assignments
- modifying role assignments
- deleting role assignments
ms.assetid: 2144c020-3253-4b47-8cda-e14c928bb471
caps.latest.revision: 52
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: d3a3526e9c52dad5c595c9df9fb722abb5f5b288
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36145778"
---
# <a name="grant-user-access-to-a-report-server-report-manager"></a>將報表伺服器的存取權授與使用者 (報表管理員)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 使用角色型安全性將報表伺服器的存取權授與使用者。 在新的報表伺服器安裝上，只有屬於本機管理員群組的成員擁有報表伺服器內容和作業的權限。 若要讓報表伺服器供其他使用者使用，您必須建立角色指派，以便將使用者或群組帳戶對應至指定工作集合的預先定義角色。  
  
 **SharePoint 模式報表伺服器：** 若為針對 SharePoint 整合模式所設定的報表伺服器，您可以設定使用 SharePoint 權限從 SharePoint 網站存取的方式。 SharePoint 網站的權限等級會決定報表伺服器內容和作業的存取權。 您必須是網站管理員，才能授與 SharePoint 網站的權限。 如需詳細資訊，請參閱 [授與 SharePoint 網站上報表伺服器項目的權限](granting-permissions-on-report-server-items-on-a-sharepoint-site.md)。  
  
 **原生模式報表伺服器：** 此主題的重點在於為原生模式所設定的報表伺服器，以及使用報表管理員將使用者指派至角色。 目前有兩種角色類型：  
  
-   項目層級角色是用來檢視、加入和管理報表伺服器內容、訂閱、報表處理，以及報表記錄。 項目層級角色指派定義於根節點 ([主資料夾] 資料夾) 或階層中更低的特定資料夾或項目上。  
  
-   系統層級角色會授與並未繫結至任何特定項目之網站範圍作業的存取權。 範例包括使用報表產生器和使用共用排程。  
  
     這兩種角色類型彼此互補，而且您應該一起使用它們。 因此，將使用者加入至報表伺服器是兩個部分的作業。 如果您將某位使用者指派至項目層級角色，就應該同時將他指派至伺服器層級角色。 指派使用者至角色時，您必須選取已經定義的角色。 若要建立、修改或刪除角色，請使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。 如需詳細資訊，請參閱[建立、 刪除或修改角色&#40;Management Studio&#41;](role-definitions-create-delete-or-modify.md)。  
  
## <a name="before-you-start"></a>開始之前  
 將使用者加入至原生模式報表伺服器之前，請檢閱下列清單。  
  
-   您在報表伺服器電腦上必須是本機管理員群組的成員。 如果您要將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 部署在 [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] 或 Windows Server 2008 上，就必須進行其他組態設定，然後才能在本機管理報表伺服器。 如需詳細資訊，請參閱[設定原生模式報表伺服器進行本機管理 &#40;SSRS&#41;](../report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)。  
  
-   若要將這項工作委派給其他使用者，請建立角色指派，以便將使用者帳戶對應至「內容管理員」和「系統管理員」角色。 擁有「內容管理員」和「系統管理員」權限的使用者可以將使用者加入至報表伺服器。  
  
-   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中，檢視「系統角色」和「使用者角色」的預先定義角色，如此您就可以熟悉每個角色的工作類型。 由於工作描述不會顯示在報表管理員中，因此在您開始加入使用者之前，應該會想要先熟悉這些角色。  
  
-   (選擇性) 您可以自訂角色或定義其他角色來包含所需的工作集合。 例如，如果您計畫針對個別項目使用自訂安全性設定，可能會想要建立新角色定義，以便授與資料夾的檢視存取權。  
  
### <a name="to-add-a-user-or-group-to-a-system-role"></a>若要將使用者或群組加入至系統角色  
  
1.  啟動[報表管理員 &#40;SSRS 原生模式&#41;](../report-manager-ssrs-native-mode.md)。  
  
2.  按一下 **[站台設定]**。  
  
3.  按一下 **[安全性]**。  
  
4.  按一下 **[新增角色指派]**。  
  
5.  在**群組或使用者名稱**中，輸入 Windows 網域使用者或群組帳戶，格式如下：\<網域 >\\< 帳戶\>。 如果您要使用表單驗證或自訂安全性，請使用適用於部署的正確格式來指定使用者或群組帳戶。  
  
6.  選取系統角色，然後按一下 **[確定]**。  
  
     由於角色是累計的，因此如果您同時選取「系統管理員」和「系統使用者」，則使用者或群組就能夠以這兩種角色來執行工作。  
  
7.  重複上述步驟，以便建立其他使用者或群組的指派。  
  
### <a name="to-add-a-user-or-group-to-an-item-role"></a>若要將使用者或群組加入至項目角色  
  
1.  啟動 **[報表管理員]** 並找出您想要加入使用者或群組的報表項目。  
  
2.  將滑鼠停留在該項目上，然後按一下下拉箭號。  
  
3.  在下拉式功能表中，按一下 [安全性]。  
  
4.  按一下 **[新增角色指派]**。  
  
    > [!NOTE]  
    >  如果某個項目目前是從父項目繼承安全性，請按一下工具列中的 **[編輯項目安全性]** 來變更安全性設定。 然後，按一下 **[新增角色指派]**。  
  
5.  在**群組或使用者名稱**中，輸入 Windows 網域使用者或群組帳戶，格式如下：\<網域 >\\< 帳戶\>。 如果您要使用表單驗證或自訂安全性，請使用適用於部署的正確格式來指定使用者或群組帳戶。  
  
6.  選取描述使用者或群組應如何存取項目的一或多個角色定義，然後按一下 **[確定]**。  
  
7.  重複上述步驟，以便建立其他使用者或群組的指派。  
  
## <a name="see-also"></a>另請參閱  
 (建立-和-管理-角色-assignments.md)   
 [新增角色指派： 編輯角色指派頁面&#40;報表管理員&#41;](../new-role-assignment-edit-role-assignment-page-report-manager.md)   
 [安全性屬性頁面，項目&#40;報表管理員&#41;](../security-properties-page-items-report-manager.md)   
 [角色指派](role-assignments.md)   
 [角色定義](role-definitions.md)  
  
  