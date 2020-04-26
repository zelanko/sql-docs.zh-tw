---
title: 建立和管理 Kpi （SSAS 表格式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.kpi.f1
ms.assetid: c96026c2-4394-4c3c-986b-4c95a4421900
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fc0bd941392c208ad693be21a391d7b9e3f587a1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "66067504"
---
# <a name="create-and-manage-kpis-ssas-tabular"></a>建立及管理 KPI (SSAS 表格式)
  本主題描述如何建立、編輯或刪除表格式模型中的 KPI (關鍵效能指標)。 若要建立 KPI，請選取評估為 KPI 基底值的量值。 然後使用 [關鍵效能指標] 對話方塊選取判斷為目標值的第二個量值或絕對值。 接著您可以定義測量基底和目標量值之間效能的狀態臨界值。  
  
 本主題也包括下列工作：  
  
-   [建立 KPI](#bkmk_create_KPI)  
  
-   [編輯 KPI](#bkmk_edit_KPI)  
  
-   [若要刪除 KPI 和基底量值](#bkmk_delete)  
  
-   [刪除 KPI，但保留基底量值](#bkmk_delete_KPI)  
  
## <a name="tasks"></a>工作  
  
> [!IMPORTANT]  
>  在建立 KPI 之前，您必須先建立判斷為值的基底量值。 接著將此基底量值延伸至 KPI。 在另一個主題中將說明如何建立量值， [建立及管理量值 &#40;SSAS 表格式&#41;](measures-ssas-tabular.md)。 KPI 也需要目標值。 此值可來自另一個預先定義的量值或絕對值。 一旦將基底量值延伸至 KPI 之後，您就可以在 [關鍵效能指標] 對話方塊中選取目標值及定義狀態臨界值。  
  
###  <a name="to-create-a-kpi"></a><a name="bkmk_create_KPI"></a>建立 KPI  
  
1.  在量值方格中，以滑鼠右鍵按一下將作為基底量值 (值) 使用的量值，然後按一下 [建立 KPI]****。  
  
2.  在 **[關鍵效能指標]** 對話方塊的 **[定義目標值]** 中，選取下列其中一項：  
  
     選取 **[量值]**，然後從清單方塊中選取目標量值。  
  
     選取 **[絕對值]**，然後輸入數值。  
  
3.  在 **[定義狀態臨界值]** 中，按一下並滑動高低臨界值。  
  
4.  在 **[選取圖示樣式]** 中，按一下影像類型。  
  
5.  按一下 **[描述]**，然後輸入 KPI、值、狀態和目標的描述。  
  
> [!TIP]  
>  您可以使用 [在 Excel 中進行分析] 功能測試 KPI。 如需詳細資訊，請參閱本主題稍後的 [在 Excel 中進行分析 &#40;SSAS 表格式&#41;](analyze-in-excel-ssas-tabular.md)中的 [角色管理員] 對話方塊來定義角色的表格式模型作者。  
  
###  <a name="to-edit-a-kpi"></a><a name="bkmk_edit_KPI"></a>編輯 KPI  
  
-   在量值方格中，以滑鼠右鍵按一下作為 KPI 基底量值 (值) 的量值，然後按一下 [編輯 KPI 設定]****。  
  
###  <a name="to-delete-a-kpi-and-the-base-measure"></a><a name="bkmk_delete"></a> 刪除 KPI 和基底量值  
  
-   在量值方格中，以滑鼠右鍵按一下作為 KPI 基底量值 (值) 的量值，然後按一下 [刪除]****。  
  
###  <a name="to-delete-a-kpi-but-keep-the-base-measure"></a><a name="bkmk_delete_KPI"></a>刪除 KPI，但保留基底量值  
  
-   在量值方格中，以滑鼠右鍵按一下作為 KPI 基底量值 (值) 的量值，然後按一下 [刪除 KPI]****。  
  
## <a name="alt-shortcuts"></a>ALT 捷徑  
  
|UI 區段|按鍵命令|  
|----------------|-----------------|  
|KPI 基準量值|ALT+B|  
|KPI 狀態|ALT+S|  
|Measure|ALT+M|  
|[絕對值]|ALT+A|  
|[定義狀態臨界值]|ALT+U|  
|[選取圖示樣式]|ALT+I|  
|趨勢|ALT+T|  
|說明|ALT+D|  
|趨勢|ALT+T|  
  
## <a name="see-also"></a>另請參閱  
 [&#40;SSAS 表格式&#41;的 Kpi](kpis-ssas-tabular.md)   
 [&#40;SSAS 表格式&#41;的量值](measures-ssas-tabular.md)   
 [建立及管理量值 &#40;SSAS 表格式&#41;](create-and-manage-measures-ssas-tabular.md)  
  
  
