---
title: "修改或刪除角色指派 (報表管理員) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- removing role assignments
- roles [Reporting Services], assignments
- system roles [Reporting Services]
- modifying role assignments
- deleting role assignments
ms.assetid: 523bdd32-92cb-4b48-a3a9-d58b2385bde7
caps.latest.revision: "45"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 7d4a89bd4ab25ed62e8add7d6290f0a51954aab3
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="role-assignments---modify-or-delete"></a>角色指派 - 修改或刪除
  角色指派會將某個群組或使用者帳戶對應至包含可執行之工作的預先定義角色定義。 它會決定某位使用者可執行的作業類型，包括資料夾、報表、模型或其他內容類型。 若要建立、修改或刪除角色指派，您可以使用報表管理員。 針對特定使用者或群組建立角色指派之後，您之後可以透過選取不同的角色，修改此指派。 如果您想要撤銷報表伺服器的權限，可以從報表伺服器中刪除角色指派。  
  
 根據您的目標而定，其他方式可能會更適合。 範例包括自訂或建立新的角色定義，或在 Active Directory 中修改群組帳戶的成員資格。  
  
 例如，假設您擁有一個使用者群組，而這些使用者需要完全管理其內容，但是不應該擁有與內容管理員相關聯的完整權限集。 在此情況下，您應該建立名為「部門內容管理員」的新角色定義，其中包含內容管理員的所有工作，但**設定項目的安全性原則**除外。  
  
 同樣地，如果您是系統或網路管理員，而且在報表管理員中管理 Active Directory 群組帳戶比角色指派更容易，就可以透過針對群組帳戶建立單一角色指派，降低管理角色指派的負擔，然後在使用者不再需要存取報表時調整群組成員資格。  
  
 如果您決定修改或刪除角色指派是最佳做法，請務必同時檢查系統角色指派和項目角色指派。 每種角色指派類型都是透過報表管理員中的不同頁面進行設定的。  
  
### <a name="to-modify-or-delete-a-system-role-assignment"></a>若要修改或刪除系統角色指派  
  
1.  啟動 [報表管理員 &#40;SSRS 原生模式&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)。  
  
2.  按一下 **[站台設定]**。  
  
3.  按一下 **[安全性]**。 如此就會依據帳戶名稱列出目前針對伺服器或向外延展部署所定義的所有系統層級角色指派。  
  
4.  尋找您想要修改或刪除的角色指派。  
  
5.  若要新增或移除特定使用者或群組的角色，請按一下 [編輯]。  
  
6.  若要刪除角色指派，請按一下使用者或群組名稱旁的核取方塊，然後按一下 [刪除]。  
  
### <a name="to-modify-or-delete-an-item-role-assignment"></a>若要修改或刪除項目角色指派  
  
1.  啟動 [報表管理員] 並找出您想要編輯或刪除角色指派的項目。  
  
2.  將滑鼠停留在該項目上，然後按一下下拉箭號。  
  
3.  在下拉式功能表中，按一下 [安全性]。  
  
4.  尋找您想要修改或刪除的角色指派。  
  
5.  若要新增或移除特定使用者或群組的角色，請按一下 [編輯]。  
  
6.  若要刪除角色指派，請按一下使用者或群組名稱旁的核取方塊，然後按一下 [刪除]。  
  
## <a name="see-also"></a>另請參閱  
 [建立和管理角色指派](../../reporting-services/security/create-and-manage-role-assignments.md)   
 [角色指派](../../reporting-services/security/role-assignments.md)   
 [網站設定頁面 &#40;報表管理員&#41;](http://msdn.microsoft.com/library/4d67a01c-eae4-49ba-a6e8-8e983c0248f5)   
 [新增系統角色指派：編輯系統角色指派頁面 &#40;報表管理員&#41;](http://msdn.microsoft.com/library/62a22ab9-1eb4-4ce5-8dd7-06b5ed2d9a2a)  
  
  
