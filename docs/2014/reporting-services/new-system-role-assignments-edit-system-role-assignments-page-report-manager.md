---
title: 新增系統角色指派： 編輯系統角色指派頁面 （報表管理員） |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 62a22ab9-1eb4-4ce5-8dd7-06b5ed2d9a2a
caps.latest.revision: 26
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 4cc3521561aac3e91e2af2dd8f45eea77b74b58e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36134540"
---
# <a name="new-system-role-assignments-edit-system-role-assignments-page-report-manager"></a>新增系統角色指派：編輯系統角色指派頁面 (報表管理員)
  使用 [新增系統角色指派] 或 [編輯系統角色指派] 頁面來定義報表伺服器的安全性。 所有的安全性都透過角色指派來定義，角色指派會對應特定使用者或群組至其可執行的工作。 以您在進行角色指派時選取的角色定義來表示工作清單。  
  
 在系統層級，您建立或修改的角色指派將整個套用至報表伺服器。 例如，建立共用排程的能力是在系統層級指定的，因為共用排程是全系統要使用的。  
  
 根據預設，Reporting Services 會提供兩個預先定義的系統層級角色：  
  
-   「系統使用者」包括允許使用者檢視報表伺服器屬性和共用排程，以及執行報表定義的工作，讓使用者能夠檢視已經發行至報表伺服器的點選連結報表。 大部分使用者都應該指派至這個角色。  
  
-   「系統管理員」包括建立和管理共用排程、設定伺服器屬性，以及為其他使用者建立系統層級角色指派的工作。 少數使用者需要這個層級的權限。  
  
## <a name="navigation"></a>導覽  
 您可以使用下列程序，在使用者介面 (UI) 中導覽至這個位置。  
  
###### <a name="to-open-the-new-system-role-assignments-or-edit-system-role-assignments-page"></a>若要開啟新增系統角色指派或編輯系統角色指派頁面  
  
1.  開啟報表管理員。  
  
2.  在頁面的頂端，按一下右邊角落的 **[站台設定]**。 這樣就會開啟該站台的 [一般] 屬性頁面。  
  
3.  選取 **[安全性]** 索引標籤。您必須擁有「內容管理員」和「系統管理員」權限才能存取此頁面。  
  
4.  若要建立新的角色指派，請在工具列中，按一下 **[新增角色指派]** 。 若要編輯現有的角色指派，請在 [安全性] 屬性頁面上，按一下群組或使用者旁的 **[編輯]** 。  
  
## <a name="options"></a>選項。  
 **群組或使用者**  
 輸入網域中之群組或使用者帳戶的名稱。 如果是以本機帳戶執行報表伺服器，您就必須指定本機群組或使用者。 如果是以網域帳戶執行報表伺服器，您就必須指定網域群組或使用者。 以此格式輸入帳戶：\<網域 >\\< 帳戶\>。  
  
> [!NOTE]  
>  這個方塊只有 [新增角色指派] 頁面才有提供。  
  
 **角色**  
 提供您可以指派給其他使用者的系統層級角色清單。 您可以針對單一角色指派指定多個角色。  
  
 報表管理員不會顯示每個角色中的工作，也不會提供加入或修改這些工作的方式。 您必須依照原本定義的方式來使用這些角色。 建立、 修改或刪除角色，請使用[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]。 如需詳細資訊，請參閱[建立、 刪除或修改角色&#40;Management Studio&#41;](security/role-definitions-create-delete-or-modify.md)。  
  
 請注意，如果您使用[!INCLUDE[ssExpressEd2005](../includes/ssexpressed2005-md.md)]with Advanced Services，您必須使用所提供的預設角色。  
  
 **描述**  
 顯示有關角色的其他資訊。 對於預先定義的角色 (如「系統使用者」或「系統管理員」)，描述會概述每一個角色支援的工作。  
  
 **刪除角色指派**  
 按一下即可刪除使用者或群組的現有角色指派。 如果它是唯一留下的角色指派，就不可以刪除該角色指派 (每一個項目至少都必須具有一個角色指派)。  
  
> [!NOTE]  
>  這個按鈕只有 [編輯角色指派] 頁面才有提供。  
  
## <a name="see-also"></a>另請參閱  
 [報表管理員 F1 說明](../../2014/reporting-services/report-manager-f1-help.md)   
 [角色指派](security/role-assignments.md)   
 [角色定義](security/role-definitions.md)  
  
  