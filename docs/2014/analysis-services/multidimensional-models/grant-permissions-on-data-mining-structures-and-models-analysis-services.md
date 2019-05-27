---
title: 授與權限的資料採礦結構和模型 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.roledesignerdialog.miningmodels.f1
helpviewer_keywords:
- data mining [Analysis Services], security
- permissions [Analysis Services], mining models
- mining models [Analysis Services], security
- mining structures [Analysis Services], security
- permissions [Analysis Services], mining structures
- user access rights [Analysis Services], mining structures
- user access rights [Analysis Services], mining models
ms.assetid: a0008004-e2b7-47db-acad-5fe7e12b130f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 25eb8fe00c523d4a94b7f6f0325bfd2c1f55e7be
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66074935"
---
# <a name="grant-permissions-on-data-mining-structures-and-models-analysis-services"></a>授與資料採礦結構和模型的權限 (Analysis Services)
  根據預設，只有 Analysis Services 伺服器管理員擁有檢視資料庫中資料採礦結構或採礦模型的權限。 請依照下列指示，授與權限給非管理員的使用者。  
  
## <a name="set-permissions-to-access-a-mining-structure"></a>設定權限以存取採礦結構  
  
1.  在 SSMS 中，連線到 Analysis Services。 如果您需要這些步驟的說明，請參閱[從用戶端應用程式連接 &#40;Analysis Services&#41;](../instances/connect-from-client-applications-analysis-services.md)。  
  
2.  在物件總管中，開啟 [資料庫] 資料夾，然後選取資料庫。  
  
3.  以滑鼠右鍵按一下 [角色]，然後選擇 [新增角色]。  
  
4.  在 [一般] 窗格中，輸入名稱，並選擇性地輸入描述。 這個頁面也包含數個資料庫權限，例如，[完整控制權]、[處理資料庫] 及 [讀取定義]。 存取資料採礦時不需要這些權限的任何一個。 如需資料庫權限的詳細資訊，請參閱[授與資料庫權限 &#40;Analysis Services&#41;](grant-database-permissions-analysis-services.md)。  
  
5.  在 [採礦結構] 窗格中，為每個資料採礦結構選取 [讀取] 或 [讀取/寫入]。  
  
6.  在 [成員資格] 窗格中，輸入使用這個角色連線到 Analysis Services 的 Windows 使用者和群組帳戶。  
  
7.  按一下 [確定]，完成角色的建立。  
  
## <a name="set-permissions-to-access-a-mining-model"></a>設定權限以存取採礦模型  
 對於資料採礦模型而言，角色可以擁有 [讀取] 或 [讀取/寫入] 權限，以及 [鑽研] 和 [讀取定義] 權限，以允許檢視和瀏覽基礎資料。  
  
 **注意**：如果您在採礦結構和採礦模型上都啟用鑽研，則任何使用者只要是對於採礦模型和採礦結構具有鑽研權限的角色成員，也都可以檢視採礦結構中的資料行，即使這些資料行未包含在採礦模型中。 因此，若要保護機密資訊，您應該設定資料來源檢視來遮罩個人資訊，並只有在必要時才允許採礦結構的鑽研存取。  
  
 若要授與資料庫角色讀取或讀取/寫入權限，使用者必須是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器角色的成員，或者擁有完整控制權 (管理員) 權限之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫角色的成員。  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體，在物件總管中展開適當資料庫的 [角色]，然後按一下資料庫角色 (或建立新的資料庫角色)。  
  
2.  在 [採礦結構] 窗格的 [採礦模型] 清單中尋找採礦模型，然後針對該採礦模型選取 [讀取]、[讀取/寫入]、[鑽研] 或 [瀏覽]。  
  
3.  在 [成員資格] 窗格中，輸入使用這個角色連接到 Analysis Services 的 Windows 使用者和群組帳戶。  
  
4.  按一下 [確定]，完成角色的建立。  
  
 若要在使用資料採礦延伸模組 (DMX) OPENQUERY 子句的鑽研查詢中使用資料來源，資料庫角色還需要對適當的資料來源物件具有讀取/寫入權限。 如需詳細資訊，請參閱[授與資料來源物件的權限 &#40;Analysis Services&#41;](grant-permissions-on-a-data-source-object-analysis-services.md) 和 [OPENQUERY &#40;DMX&#41;](/sql/dmx/source-data-query-openquery)。  
  
> [!NOTE]  
>  依預設，使用 OPENROWSET 來提交 DMX 查詢的功能已停用。  
  
## <a name="see-also"></a>另請參閱  
 [授與伺服器系統管理員權限&#40;Analysis Services&#41;](../instances/grant-server-admin-rights-to-an-analysis-services-instance.md)   
 [授與 Cube 或模型權限 &#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md)   
 [授與維度資料的自訂存取權 &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md)   
 [授與資料格資料的自訂存取權 &#40;Analysis Services&#41;](grant-custom-access-to-cell-data-analysis-services.md)  
  
  
