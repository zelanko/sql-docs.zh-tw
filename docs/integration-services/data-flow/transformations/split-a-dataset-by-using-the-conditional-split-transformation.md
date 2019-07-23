---
title: 使用條件式分割轉換來分割資料集 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Conditional Split transformation
- splitting dataset
- datasets [Integration Services], splitting
ms.assetid: 23b3e84f-9296-4dc9-81c0-c7f06ae3f1ff
author: janinezhang
ms.author: janinez
ms.openlocfilehash: d6342cf8409a9133a5e21205b0864af97ceeac75
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67928101"
---
# <a name="split-a-dataset-by-using-the-conditional-split-transformation"></a>使用條件式分割轉換來分割資料集

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  若要加入及設定「條件式分割」轉換，封裝中必須已包含至少一個「資料流程」工作和一個來源。  
  
### <a name="to-conditionally-split-a-dataset"></a>若要條件式分割資料集  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 **[資料流程]** 索引標籤，然後從 **[工具箱]** 拖曳「條件式分割」轉換至設計介面。  
  
4.  從來源或先前的轉換將連接子拖曳到「條件式分割」轉換，以便將「條件式分割」轉換連接到資料流程。  
  
5.  按兩下「條件式分割」轉換。  
  
6.  在 **[條件式分割轉換編輯器]** 中，拖曳變數、資料行、函數和運算子到方格中的 **[條件]** 資料行，以建立要當作條件使用的運算式。 或者，您也可以在 **[條件]** 資料行中輸入運算式。  
  
    > [!NOTE]  
    >  變數或資料行可以用在多個運算式中。  
  
    > [!NOTE]  
    >  如果運算式無效，則運算式文字會反白顯示，且資料行上的「工具提示」會描述錯誤。  
  
7.  (選擇性) 修改 **[輸出名稱]** 資料行中的值。 預設名稱為 Case 1、Case 2 等等。  
  
8.  若要修改評估條件的順序，請按一下向上鍵或向下鍵。  
  
    > [!NOTE]  
    >  將最可能遇到的條件放在清單的最上方。  
  
9. (選擇性) 修改不符合任何條件之資料列的預設輸出名稱。  
  
10. 若要設定錯誤輸出，請按一下 **[設定錯誤輸出]** 。 如需詳細資訊，請參閱 [偵錯資料流程](../../../integration-services/troubleshooting/debugging-data-flow.md)。  
  
11. 按一下 [確定]  。  
  
12. 若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
## <a name="see-also"></a>另請參閱  
 [Conditional Split Transformation](../../../integration-services/data-flow/transformations/conditional-split-transformation.md)   
 [Integration Services 轉換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services 路徑](../../../integration-services/data-flow/integration-services-paths.md)   
 [Integration Services 資料類型](../../../integration-services/data-flow/integration-services-data-types.md)   
 [資料流程工作](../../../integration-services/control-flow/data-flow-task.md)   
 [Integration Services &#40;SSIS&#41; 運算式](../../../integration-services/expressions/integration-services-ssis-expressions.md)  
  
  
