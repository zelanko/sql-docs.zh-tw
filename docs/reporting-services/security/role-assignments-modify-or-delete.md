---
title: 修改或刪除角色指派 (SSRS Web 入口網站) | Microsoft Docs
ms.date: 05/07/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- removing role assignments
- roles [Reporting Services], assignments
- system roles [Reporting Services]
- modifying role assignments
- deleting role assignments
ms.assetid: 523bdd32-92cb-4b48-a3a9-d58b2385bde7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 28695a4849b29c6e593f42489fc149efd9a8db53
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65570650"
---
# <a name="role-assignments---modify-or-delete"></a>角色指派 - 修改或刪除

角色指派會將某個群組或使用者帳戶對應至預先定義的角色，此角色可定義能夠完成的工作。 它會決定某位使用者可執行的工作類型，包括資料夾、報表、模型或其他內容類型。 若要建立、修改或刪除角色指派，您可以使用 SSRS Web 入口網站。 針對特定使用者或群組建立角色指派之後，您之後可以透過選取不同的角色，修改此指派。 如果您想要撤銷報表伺服器的權限，可以從報表伺服器中刪除角色指派。  

根據您的目標而定，其他方式可能會更適合。 範例包括自訂或建立新的角色定義，或在 Active Directory 中修改群組帳戶的成員資格。  

例如，假設您擁有一個使用者群組，而這些使用者需要管理其內容，但是不應該擁有與內容管理員相關聯的完整權限集。 您可以建立一個稱為「部門內容管理員」的新角色定義。 它可以包含內容管理員中的所有工作，但**設定項目的安全性原則**除外。

同樣地，如果您是系統或網路管理員，對您來說，管理 Active Directory 群組帳戶可能比管理入口網站中的角色指派還容易。 您可以為一個群組帳戶建立單一角色指派，以減少管理角色指派的負擔。 接著，您可以在使用者不再需要存取報表時，修改群組成員資格。
  
 如果您確定修改或刪除角色指派是最佳做法，請記得同時檢查系統角色和項目角色指派。 每種類型的角色指派都是透過入口網站中的不同頁面設定的。
  
## <a name="to-modify-or-delete-a-system-role-assignment"></a>若要修改或刪除系統角色指派
  
1. 存取[報表伺服器的入口網站 &#40;SSRS 原生模式&#41;](../../reporting-services/web-portal-ssrs-native-mode.md)。

2. 選取 [站台設定]   > [安全性]  。 如此就會依據帳戶名稱列出目前針對伺服器或向外延展部署所定義的所有系統層級角色指派。

3. 尋找您想要修改或刪除的角色指派。

4. 若要新增或移除特定使用者或群組的角色，選取 [編輯]  。

5. 若要刪除角色指派，選取使用者或群組名稱旁的核取方塊，然後選取 [刪除]  。

### <a name="to-modify-or-delete-an-item-role-assignment"></a>若要修改或刪除項目角色指派

1. 存取入口網站，並找出您想要編輯或刪除角色指派的項目。

2. 將滑鼠停留在該項目上，然後選取下拉箭號。

3. 在下拉式功能表中選取 [安全性]  。

4. 尋找您想要修改或刪除的角色指派。

5. 若要新增或移除特定使用者或群組的角色，選取 [編輯]  。

6. 若要刪除角色指派，選取使用者或群組名稱旁的核取方塊，然後選取 [刪除]  。

## <a name="see-also"></a>另請參閱

[建立及管理角色指派](../../reporting-services/security/create-and-manage-role-assignments.md)  
[角色指派](../../reporting-services/security/role-assignments.md)  
