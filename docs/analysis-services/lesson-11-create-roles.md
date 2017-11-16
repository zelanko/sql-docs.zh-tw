---
title: "第 12 課： 建立角色 |Microsoft 文件"
ms.custom: 
ms.date: 03/27/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 984face4-00fc-46d3-8ae1-9755bf737bdf
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 659b8bb8af4d759367d81bb3e8828360fd2b1f28
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-11-create-roles"></a>第 11 課： 建立角色
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

在這一課，您將建立角色。 角色會藉由僅限身為角色成員的 Windows 使用者存取的方式，提供模型資料庫物件和資料安全性。 每個角色都會定義一項權限：「無」、「讀取」、「讀取和處理」、「處理」或「系統管理員」。 可以使用 角色管理員模型撰寫期間定義角色。 部署模型之後，您可以使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]管理角色。 若要進一步了解，請參閱[角色](../analysis-services/tabular-models/roles-ssas-tabular.md)。  
  
> [!NOTE]  
> 建立角色不是完成本教學課程的必要工作。 根據預設，您目前用來登入的帳戶將擁有模型的系統管理員權限。 不過，若要讓其他使用者在您的組織使用報表用戶端來瀏覽此模型中，您必須建立至少一個角色具有讀取權限，並將這些使用者新增為成員。  
  
您將建立三個角色：  
  
-   **銷售經理**– 此角色可包含您要的讀取權限的所有模型物件和資料的組織中的使用者。  
  
-   **Sales Analyst US** – 此角色可包含您想只能夠瀏覽與美國銷售額相關資料的組織中的使用者。 針對此角色，您將使用 DAX 公式定義「資料列篩選」，限制成員僅瀏覽美國的資料。  
  
-   **系統管理員**– 此角色可包含您想要有系統管理員權限，允許無限制的存取和 model 資料庫上執行管理工作的權限的使用者。  
  
由於組織中的 Windows 使用者和群組帳戶是唯一的，因此您可以將帳戶從特定組織加入至成員。 不過，針對此教學課程，您也可以將成員留空。 您稍後仍然能夠在第 12 課：「在 Excel 中進行分析」中測試每個角色的效用。  
  
完成本課程的估計時間： **15 分鐘**  
  
## <a name="prerequisites"></a>必要條件  
本主題是表格式模型教學課程的一部分，必須依序完成。 然後再執行工作，在這一課，您應已完成上一課：[第 10 課： 建立資料分割](../analysis-services/lesson-10-create-partitions.md)。  
  
## <a name="create-roles"></a>建立角色  
  
#### <a name="to-create-a-sales-manager-user-role"></a>若要建立 Sales Manager 使用者角色  
  
1.  在表格式模型總管 中，以滑鼠右鍵按一下**角色** > **角色**。  
  
2.  在 [角色管理員] 中，按一下**新增**。  
  
3.  按一下新角色，然後在**名稱**資料行中，若要將角色重新命名**銷售經理**。  
  
4.  按一下 [權限] 資料行中的下拉式清單，然後選取 [讀取] 權限。 

    ![做為表格式-lesson11-新的角色](../analysis-services/media/as-tabular-lesson11-new-role.png) 
  
5.  選擇性： 按一下**成員**索引標籤，然後再按一下**新增**。 在 [選取使用者或群組] 對話方塊中，從組織輸入要包含在角色中的 Windows 使用者或群組。  
  
#### <a name="to-create-a-sales-analyst-us-user-role"></a>若要建立 Sales Analyst US 使用者角色  
  
1.  在 [角色管理員] 中，按一下**新增**。    
  
2.  若要將角色重新命名**Sales Analyst US**。  
  
3.  授與此角色**讀取**權限。  
  
4.  按一下 [資料列篩選器] 索引標籤，然後再針對**DimGeography**資料表，在 [DAX 篩選] 欄位中輸入下列公式：  
  
    ```
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    資料列篩選公式必須解析布林 (TRUE/FALSE) 值。 您要使用此公式指定使用者只能看到 Country Region Code 值為 “US” 的資料列。  
    ![做為表格式-lesson11-角色-篩選](../analysis-services/media/as-tabular-lesson11-role-filter.png) 
  
6.  選擇性：按一下 [成員] 索引標籤，然後按一下 [新增]。 在 [選取使用者或群組] 對話方塊中，從組織輸入要包含在角色中的 Windows 使用者或群組。  
  
#### <a name="to-create-an-administrator-user-role"></a>若要建立的系統管理員使用者角色  
  
1.  按一下 **[新增]**。  
  
2.  若要將角色重新命名**管理員**。  
  
3.  授與此角色**管理員**權限。  
  
4.  選擇性：按一下 [成員] 索引標籤，然後按一下 [新增]。 在 [選取使用者或群組] 對話方塊中，從組織輸入要包含在角色中的 Windows 使用者或群組。 
  
  
## <a name="whats-next"></a>下一步
移至下一課：[第 12 課： 在 Excel 中分析](../analysis-services/lesson-12-analyze-in-excel.md)。

  
  

