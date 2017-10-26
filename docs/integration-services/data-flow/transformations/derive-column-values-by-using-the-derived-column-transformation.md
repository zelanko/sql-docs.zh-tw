---
title: "使用衍生的資料行轉換來衍生資料行值 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- columns [Integration Services]
- derived columns
- columns [Integration Services], values
- Derived Column transformation
ms.assetid: 28b07746-fc6f-42b2-b741-9de6fac3f29c
caps.latest.revision: 48
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: c0106d70fa5a3b31f0a92edf5c7088cf427c59a8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/28/2017

---
# <a name="derive-column-values-by-using-the-derived-column-transformation"></a>使用衍生的資料行轉換來衍生資料行值
  若要加入及設定「衍生的資料行」轉換，封裝中必須已包含至少一個「資料流程」工作和一個來源。  
  
 「衍生的資料行」轉換使用運算式更新現有的值或將值加入至新的資料行。 若您選擇將值加入至新的資料行， **[衍生的資料行轉換編輯器]** 對話方塊就會評估運算式並定義資料行的中繼資料。 例如，如果運算式串連兩個資料行 (兩個資料行都使用 DT_WSTR 資料類型且長度為 50)，而且兩個資料行值之間會有空格，新的資料行會具有 DT_WSTR 資料類型且長度為 101。 您可以更新新資料行的資料類型。 唯一的要求就是該資料類型必須與插入的資料相容。 舉例來說，若您指派日期值到整數資料類型的資料行， **[衍生的資料行轉換編輯器]** 對話方塊就會產生驗證錯誤。 視您選擇的資料類型而定，您可指定資料行的長度、有效位數、小數位數和字碼頁。  
  
### <a name="to-derive-column-values"></a>若要衍生資料行值  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 **[資料流程]** 索引標籤，然後從 **[工具箱]**拖曳「衍生的資料行」轉換至設計介面。  
  
4.  從來源或先前的轉換將連接子拖曳到「衍生的資料行」轉換，以便將「衍生的資料行」轉換連接到資料流程。  
  
5.  按兩下「衍生的資料行」轉換。  
  
6.  在 **[衍生的資料行轉換編輯器]** 對話方塊中，拖曳變數、資料行、函數和運算子到方格中的 **[運算式]** 資料行，以建立要當作條件使用的運算式。 或者，您也可以在 **[運算式]** 資料行中輸入運算式。  
  
    > [!NOTE]  
    >  如果運算式無效，則運算式文字會反白顯示，且資料行上的「工具提示」會描述錯誤。  
  
7.  在**衍生的資料行**清單中，選取**\<新增為新的資料行 >**運算式的評估結果寫入新的資料行，或選取要以評估結果更新現有的資料行。  
  
     如果您選擇使用新資料行， **[衍生的資料行轉換編輯器]** 對話方塊就會依據資料類型、長度、有效位數、小數位數和字碼頁，評估運算式並指派資料類型到資料行。  
  
8.  如果使用新的資料行，請在 **[資料類型]** 清單中選取資料類型。 根據選取的資料類型而定，選擇性地更新 **[長度]**、 **[有效位數]**、 **[小數位數]**和 **[字碼頁]** 資料行中的值。 現有資料行的中繼資料無法變更。  
  
9. (選擇性) 修改 **[衍生的資料行名稱]** 資料行中的值。  
  
10. 若要設定錯誤輸出，請按一下 **[設定錯誤輸出]**。 如需詳細資訊，請參閱 [偵錯資料流程](../../../integration-services/troubleshooting/debugging-data-flow.md)。  
  
11. 按一下 **[確定]**。  
  
12. 若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
## <a name="see-also"></a>另請參閱  
 [Derived Column Transformation](../../../integration-services/data-flow/transformations/derived-column-transformation.md)   
 [Integration Services 資料類型](../../../integration-services/data-flow/integration-services-data-types.md)   
 [Integration Services 轉換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services 路徑](../../../integration-services/data-flow/integration-services-paths.md)   
 [資料流程工作](../../../integration-services/control-flow/data-flow-task.md)   
 [Integration Services &#40;SSIS &#41;運算式](../../../integration-services/expressions/integration-services-ssis-expressions.md)  
  
  

