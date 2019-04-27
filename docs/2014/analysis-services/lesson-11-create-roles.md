---
title: 第 12 課：建立角色 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 984face4-00fc-46d3-8ae1-9755bf737bdf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4eec5e4f93a085ab784135593c139410f5911e1e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62729621"
---
# <a name="lesson-12-create-roles"></a>第 12 課：建立角色
  在這一課，您將建立角色。 角色會藉由僅限身為角色成員的 Windows 使用者存取的方式，提供模型資料庫物件和資料安全性。 每個角色定義單一權限：無、 讀取、 讀取和處理程序、 處理序或系統管理員。 您可以使用 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中的 [角色管理員] 對話方塊，在模型撰寫期間定義角色。 部署模型之後，您可以使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 管理角色。 如需詳細資訊，請參閱[角色 &#40;SSAS 表格式&#41;](tabular-models/roles-ssas-tabular.md)。  
  
> [!NOTE]  
>  建立角色不是完成本教學課程的必要工作。 根據預設，您目前用來登入的帳戶將擁有模型的系統管理員權限。 不過，為了讓組織中的其他使用者能夠使用報表用戶端應用程式瀏覽模型，您必須至少建立一個具有「讀取」權限的角色，並將這些使用者加入為成員。  
  
 您將建立三個角色：  
  
-   銷售經理-此角色可包含使用者在您的組織，您想要的讀取權限的所有模型物件和資料。  
  
-   Sales Analyst US-此角色可包含使用者在組織想只能夠瀏覽到位於美國 (United States) 的銷售相關資料。 針對此角色，您將使用 DAX 公式定義「資料列篩選」，限制成員僅瀏覽美國的資料。  
  
-   系統管理員-此角色可包含您想要有系統管理員權限，無限制的存取權和 model 資料庫上執行管理工作的權限的使用者。  
  
 由於組織中的 Windows 使用者和群組帳戶是唯一的，因此您可以將帳戶從特定組織加入至成員。 不過，針對此教學課程，您也可以將成員留空。 您仍然可以稍後在第 12 課中測試每個角色的效果：在 Excel 中進行分析。  
  
 估計的時間才能完成這一課：**15 分鐘**  
  
## <a name="prerequisites"></a>先決條件  
 本主題是表格式模型教學課程的一部分，必須依序完成。 執行工作之前在這一課，您應已完成上一課：[第 11 課：建立分割區](lesson-10-create-partitions.md)。  
  
## <a name="create-roles"></a>建立角色  
  
#### <a name="to-create-a-sales-manager-user-role"></a>若要建立 Sales Manager 使用者角色  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中，按一下 [模型] 功能表，然後按一下 [角色]。  
  
2.  在 [角色管理員] 對話方塊中，按一下 [新增]。  
  
     具有「無」權限的新角色就會加入至清單中。  
  
3.  按一下新角色，然後在**名稱**資料行中，重新命名角色`Internet Sales Manager`。  
  
4.  按一下 [權限] 資料行中的下拉式清單，然後選取 [讀取] 權限。  
  
5.  選擇性：按一下 [成員] 索引標籤，然後按一下 [新增]。  
  
6.  在 [選取使用者或群組] 對話方塊中，從組織輸入要包含在角色中的 Windows 使用者或群組。  
  
7.  確認您的選取，然後按一下 [確定]。  
  
#### <a name="to-create-a-sales-analyst-us-user-role"></a>若要建立 Sales Analyst US 使用者角色  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中，按一下 [模型] 功能表，然後按一下 [角色]。  
  
2.  在 [角色管理員] 對話方塊中，按一下 [新增]。  
  
     具有「無」權限的新角色就會加入至清單中。  
  
3.  按一下新角色，然後在**名稱**資料行中，重新命名角色`Internet Sales US`。  
  
4.  按一下 [權限] 資料行中的下拉式清單，然後選取 [讀取] 權限。  
  
5.  按一下 [資料列篩選] 索引標籤，然後僅針對 [Geography] 資料表，在 [DAX 篩選] 資料行中輸入下列公式：  
  
     `=Geography[Country Region Code] = "US"`  
  
     資料列篩選公式必須解析布林 (TRUE/FALSE) 值。 使用此公式，就指定的資料列的 Country Region Code 值為"US"會顯示給使用者。  
  
     完成建立公式時，按 ENTER。  
  
6.  選擇性：按一下 [成員] 索引標籤，然後按一下 [新增]。  
  
7.  在 [選取使用者或群組] 對話方塊中，從組織輸入要包含在角色中的 Windows 使用者或群組。  
  
8.  確認您的選取，然後按一下 [確定]。  
  
#### <a name="to-create-an-administrator-role"></a>若要建立 Administrator 角色  
  
1.  在 [角色管理員] 對話方塊中，按一下 [新增]。  
  
2.  按一下新角色，然後在**名稱**資料行中，重新命名角色`Internet Sales Administrator`。  
  
3.  按一下 [權限] 資料行中的下拉式清單，然後選取 [系統管理員] 權限。  
  
4.  按一下 [成員] 索引標籤，然後按一下 [新增]。  
  
5.  選擇性：在 [選取使用者或群組] 對話方塊中，從組織輸入要包含在角色中的 Windows 使用者或群組。  
  
6.  確認您的選取，然後按一下 [確定]。  
  
## <a name="next-steps"></a>後續步驟  
 若要繼續本教學課程，請移至下一課：課程：[第 13 課：在 Excel 中分析](lesson-12-analyze-in-excel.md)。  
  
  
