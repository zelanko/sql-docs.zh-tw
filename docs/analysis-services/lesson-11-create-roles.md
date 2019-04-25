---
title: 第 12 課：建立角色 |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a2f507e9f22e4d090407b0b0849f69a8e7914e8d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62469127"
---
# <a name="lesson-11-create-roles"></a>第 11 課：建立角色
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

在這一課，您將建立角色。 角色會藉由僅限身為角色成員的 Windows 使用者存取的方式，提供模型資料庫物件和資料安全性。 每個角色定義單一權限：無、 讀取、 讀取和處理程序、 處理序或系統管理員。 可以使用角色管理員的模型製作期間定義角色。 部署模型之後，您可以使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]管理角色。 若要進一步了解，請參閱[角色](../analysis-services/tabular-models/roles-ssas-tabular.md)。  
  
> [!NOTE]  
> 建立角色不是完成本教學課程的必要工作。 根據預設，您目前用來登入的帳戶將擁有模型的系統管理員權限。 不過，若要讓其他使用者在您的組織使用報表用戶端瀏覽此模型中，您必須建立至少一個角色具有讀取權限，並將這些使用者新增為成員。  
  
您將建立三個角色：  
  
-   **銷售經理**-此角色可包含您要的讀取權限的所有模型物件和資料的組織中的使用者。  
  
-   **美國銷售分析師**-此角色可包含您想只能夠瀏覽至美國境內銷售相關資料的組織中的使用者。 針對此角色，您將使用 DAX 公式定義「資料列篩選」，限制成員僅瀏覽美國的資料。  
  
-   **系統管理員**-此角色可包含您想要有系統管理員權限，無限制的存取權和 model 資料庫上執行管理工作的權限的使用者。  
  
由於組織中的 Windows 使用者和群組帳戶是唯一的，因此您可以將帳戶從特定組織加入至成員。 不過，針對此教學課程，您也可以將成員留空。 您仍然可以稍後在第 12 課中測試每個角色的效果：在 Excel 中進行分析。  
  
估計的時間才能完成這一課：**15 分鐘**  
  
## <a name="prerequisites"></a>先決條件  
本主題是表格式模型教學課程的一部分，必須依序完成。 執行工作之前在這一課，您應已完成上一課：[第 10 課：建立分割區](../analysis-services/lesson-10-create-partitions.md)。  
  
## <a name="create-roles"></a>建立角色  
  
#### <a name="to-create-a-sales-manager-user-role"></a>若要建立 Sales Manager 使用者角色  
  
1.  在表格式模型總管 中，以滑鼠右鍵按一下**角色** > **角色**。  
  
2.  在 [角色管理員] 中，按一下**新增**。  
  
3.  按一下新角色，然後在**名稱**資料行中，重新命名角色**銷售經理**。  
  
4.  按一下 [權限] 資料行中的下拉式清單，然後選取 [讀取] 權限。 

    ![as-tabular-lesson11-new-role](../analysis-services/media/as-tabular-lesson11-new-role.png) 
  
5.  選擇性：按一下 **成員**索引標籤，然後再按一下**新增**。 在 [選取使用者或群組] 對話方塊中，從組織輸入要包含在角色中的 Windows 使用者或群組。  
  
#### <a name="to-create-a-sales-analyst-us-user-role"></a>若要建立 Sales Analyst US 使用者角色  
  
1.  在 [角色管理員] 中，按一下**新增**。    
  
2.  重新命名角色，才能**美國銷售分析師**。  
  
3.  授與此角色**讀取**權限。  
  
4.  按一下 [資料列篩選器] 索引標籤，然後針對**DimGeography**資料表，在 [DAX 篩選] 欄位中輸入下列公式：  
  
    ```
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    資料列篩選公式必須解析布林 (TRUE/FALSE) 值。 使用此公式，就指定的資料列的 Country Region Code 值為"US"會顯示給使用者。  
    ![as-tabular-lesson11-role-filter](../analysis-services/media/as-tabular-lesson11-role-filter.png) 
  
6.  選擇性：按一下 [成員] 索引標籤，然後按一下 [新增]。 在 [選取使用者或群組] 對話方塊中，從組織輸入要包含在角色中的 Windows 使用者或群組。  
  
#### <a name="to-create-an-administrator-user-role"></a>若要建立的系統管理員使用者角色  
  
1.  按一下 **[新增]**。  
  
2.  重新命名角色，才能**系統管理員**。  
  
3.  授與此角色**系統管理員**權限。  
  
4.  選擇性：按一下 [成員] 索引標籤，然後按一下 [新增]。 在 [選取使用者或群組] 對話方塊中，從組織輸入要包含在角色中的 Windows 使用者或群組。 
  
  
## <a name="whats-next"></a>下一步
請移至下一課：[第 12 課：在 Excel 中分析](../analysis-services/lesson-12-analyze-in-excel.md)。

  
  
