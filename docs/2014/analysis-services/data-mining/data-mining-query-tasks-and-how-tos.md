---
title: 資料採礦查詢工作和使用說明 |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models [Analysis Services], how-to topics
ms.assetid: 1bc2a775-6e62-4c66-a53c-201f2ea66295
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 24ccf065a393e9534f3f4a3f830f90e3d1d5e5cc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66084952"
---
# <a name="data-mining-query-tasks-and-how-tos"></a>資料採礦查詢工作和使用說明
  建立查詢的功能對於使用資料採礦模型十分重要。 本節提供一些範例連結，這些範例示範如何透過使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中提供的工具針對資料採礦模型建立查詢。 如果您需要有關資料採礦查詢的作用或者可建立之不同查詢類型的詳細資訊，請參閱 [資料採礦查詢](data-mining-queries.md)。  
  
## <a name="creating-queries-with-prediction-query-builder"></a>使用預測查詢產生器建立查詢  
 預測查詢產生器在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中都有提供，做為以圖形方式針對資料採礦模型建立查詢的方法。 下列主題說明如何選取模型、指定資料來源、自訂預測和儲存輸出。  
  
-   [使用預測查詢產生器來建立預測查詢](create-a-prediction-query-using-the-prediction-query-builder.md)  
  
-   [在資料採礦設計師中建立單一查詢](create-a-singleton-query-in-the-data-mining-designer.md)  
  
-   [使用預測查詢產生器來建立預測查詢](create-a-prediction-query-using-the-prediction-query-builder.md)  
  
-   [檢視及儲存預測查詢的結果](view-and-save-the-results-of-a-prediction-query.md)  
  
-   [手動編輯預測查詢](manually-edit-a-prediction-query.md)  
  
-   [將預測函數套用至模型](apply-prediction-functions-to-a-model.md)  
  
-   [為預測查詢選擇和對應輸入資料](choose-and-map-input-data-for-a-prediction-query.md)  
  
## <a name="using-other-data-mining-query-tools"></a>使用其他資料採礦查詢工具  
 除了使用預測查詢產生器之外，您也可以使用 DMX 或使用 XMLA 將查詢直接輸入 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中。 您還可以透過程式設計方式建立預測查詢並且將這些查詢傳送至 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器。 下列主題提供有關如何在預測查詢產生器之外建立和使用預測查詢的詳細資訊。  
  
 [根據範本建立單一預測查詢](create-a-singleton-prediction-query-from-a-template.md)  
 描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的工具來建立和執行預測查詢。  
  
 [根據範本建立單一預測查詢](create-a-singleton-prediction-query-from-a-template.md)  
 描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 所提供的範本，將參數加入預測查詢。  
  
 [針對資料採礦查詢變更逾時值](change-the-time-out-value-for-data-mining-queries.md)  
 描述如何設定伺服器的屬性，以便控制資料採礦查詢的相關行為。  
  
 [建立採礦模型內容查詢](create-a-content-query-on-a-mining-model.md)  
 描述如何使用資料採礦結構描述資料列集來建立查詢，以便傳回採礦模型中所儲存的詳細資訊。  
  
 [使用 XMLA 建立資料採礦查詢](create-a-data-mining-query-by-using-xmla.md)  
 描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的 XMLA 範本，針對採礦模型內容建立查詢。  
  
## <a name="see-also"></a>另請參閱  
 [查詢及運算式語言參考 &#40;Analysis Services&#41;](https://msdn.microsoft.com/library/gg492188(SQL.130).aspx)   
 [資料採礦預存程序 &#40;Analysis Services - 資料採礦&#41;](/sql/analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining)  
  
  
