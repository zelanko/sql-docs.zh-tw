---
title: 警告 （資料庫設計工具） (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.databasedesigner.warnings.f1
ms.assetid: 13f58b4d-f345-4fbc-ae2d-b3c8290a797d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d83620c0c6463bd6e752f65a97b2fb14e1d1c03f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48074378"
---
# <a name="warnings-database-designer-analysis-services---multidimensional-data"></a>警告 (資料庫設計工具) (Analysis Services - 多維度資料)
  使用 [警告] 索引標籤，即可檢視和解除全域規則，以及檢視和重新啟用已解除警告的特定執行個體。 **[警告]** 索引標籤會顯示兩個方格： **[設計警告規則]** 和 **[已解除的警告]**。  
  
 **若要顯示 [警告] 索引標籤**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中開啟 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 專案。  
  
2.  在方案總管中，以滑鼠右鍵按一下 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 專案，並按一下 [編輯資料庫]，然後按一下 [警告] 索引標籤。  
  
## <a name="design-warning-rules-grid"></a>設計警告規則方格  
 **[設計警告規則]** 方格會顯示所有設計警告規則。 此外，這個方格也會控制哪些規則會針對資料庫啟用。 若要啟用或停用警告規則，請選取或清除其核取方塊。  
  
 **[設計警告規則]** 方格具有下列資料行：  
  
 **說明**  
 顯示規則的名稱。 規則會依類別分組。  
  
 **重要性**  
 顯示指派給規則的重要性。  
  
 **註解**  
 (選擇性) 允許使用者輸入註解，以便說明解除警告的原因。  
  
## <a name="dismissed-warnings-grid"></a>已解除的警告方格  
 **[已解除的警告]** 方格會顯示所有已經從 **[錯誤清單]** 中解除的特定警告項目。 若要重新啟用警告，請在方格中選取它，然後按一下 [重新啟用]。  
  
 **[已解除的警告]** 方格具有下列項目：  
  
 **物件**  
 顯示代表物件類型和物件名稱的圖示。  
  
 **型別**  
 顯示物件類型。  
  
 **說明**  
 顯示規則的名稱。  
  
 **重要性**  
 顯示指派給規則的重要性。  
  
 **註解**  
 顯示解除警告時所輸入的註解。 您可以在此新增或修改註解。  
  
 **重新啟用**  
 重新啟用選取的警告。  
  
> [!NOTE]  
>  如果某個物件具有警告，但是該物件處於無效狀態中，或者您已經手動從專案中移除該物件，則清單中的警告旁邊就會顯示一個錯誤圖示。 若要解除警告，請選取它，然後按一下 [重新啟用]。  
  
## <a name="see-also"></a>另請參閱  
 [解除警告對話方塊&#40;Analysis Services-多維度資料&#41;](dismiss-warning-dialog-box-analysis-services-multidimensional-data.md)   
 [一般&#40;資料庫設計工具&#41; &#40;Analysis Services-多維度資料&#41;](general-database-designer-analysis-services-multidimensional-data.md)  
  
  
