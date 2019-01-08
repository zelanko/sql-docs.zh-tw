---
title: 建立及管理 Analysis Services 表格式模型中的 Kpi |Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1ae17e727367b702967ec879ed8469973ab3b812
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2018
ms.locfileid: "53072085"
---
# <a name="create-and-manage-kpis"></a>建立及管理 Kpi 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  本文說明如何建立、 編輯或刪除表格式模型中的 KPI （關鍵效能指標）。 若要建立 KPI，您可以選取的量值會評估為 KPI 基底值。 然後使用 [關鍵效能指標] 對話方塊選取判斷為目標值的第二個量值或絕對值。 接著您可以定義測量基底和目標量值之間效能的狀態臨界值。  
  
## <a name="tasks"></a>工作  
  
> [!IMPORTANT]  
>  在建立 KPI 之前，您必須先建立判斷為值的基底量值。 接著將此基底量值延伸至 KPI。 另一個主題，說明如何建立量值[建立及管理量值](../../analysis-services/tabular-models/create-and-manage-measures-ssas-tabular.md)。 KPI 也需要目標值。 此值可來自另一個預先定義的量值或絕對值。 一旦將基底量值延伸至 KPI 之後，您就可以在 [關鍵效能指標] 對話方塊中選取目標值及定義狀態臨界值。  
  
###  <a name="bkmk_create_KPI"></a> 建立 KPI  
  
1.  在量值方格中，以滑鼠右鍵按一下將作為基底量值 (值) 使用的量值，然後按一下 [建立 KPI]。  
  
2.  在 **[關鍵效能指標]** 對話方塊的 **[定義目標值]** 中，選取下列其中一項：  
  
     選取 **[量值]**，然後從清單方塊中選取目標量值。  
  
     選取 **[絕對值]**，然後輸入數值。  
  
3.  在 **[定義狀態臨界值]** 中，按一下並滑動高低臨界值。  
  
4.  在 **[選取圖示樣式]** 中，按一下影像類型。  
  
5.  按一下 **[描述]**，然後輸入 KPI、值、狀態和目標的描述。  
  
> [!TIP]  
>  您可以使用 [在 Excel 中進行分析] 功能測試 KPI。 如需詳細資訊，請參閱 <<c0> [ 在 Excel 中的進行分析](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)。  
  
###  <a name="bkmk_edit_KPI"></a> 編輯 KPI  
  
-   在量值方格中，以滑鼠右鍵按一下作為 KPI 基底量值 (值) 的量值，然後按一下 [編輯 KPI 設定]。  
  
###  <a name="bkmk_delete"></a> 刪除 KPI 和基底量值  
  
-   在量值方格中，以滑鼠右鍵按一下作為 KPI 基底量值 (值) 的量值，然後按一下 [刪除]。  
  
###  <a name="bkmk_delete_KPI"></a> 刪除 KPI，但保留基底量值  
  
-   在量值方格中，以滑鼠右鍵按一下作為 KPI 基底量值 (值) 的量值，然後按一下 [刪除 KPI]。  
  
## <a name="alt-shortcuts"></a>ALT 捷徑  
  
|UI 區段|按鍵命令|  
|----------------|-----------------|  
|KPI 基準量值|ALT+B|  
|KPI 狀態|ALT+S|  
|[量值]|ALT+M|  
|[絕對值]|ALT+A|  
|[定義狀態臨界值]|ALT+U|  
|[選取圖示樣式]|ALT+I|  
|趨勢|ALT+T|  
|說明|ALT+D|  
|趨勢|ALT+T|  
  
## <a name="see-also"></a>另請參閱  
 [Kpi](../../analysis-services/tabular-models/kpis-ssas-tabular.md)   
 [量值](../../analysis-services/tabular-models/measures-ssas-tabular.md)   
 [建立和 managemeasures](../../analysis-services/tabular-models/create-and-manage-measures-ssas-tabular.md)  
  
  
