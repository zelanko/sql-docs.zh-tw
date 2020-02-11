---
title: 查詢（SQL Server 資料採礦增益集） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- queries [data mining]
- Data Mining Query Advanced Editor
- query builder [data mining]
- DMX
ms.assetid: 16af4a6f-18d4-496a-a304-7a13aa32ee76
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dcddeb64b14301f08a7dc723ef89737102f257ad
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66070474"
---
# <a name="query-sql-server-data-mining-add-ins"></a>查詢 (SQL Server 資料採礦增益集)
  ![資料採礦功能區中的查詢模型按鈕](media/dmc-query.gif "資料採礦功能區中的查詢模型按鈕")  
  
 **查詢**嚮導可協助您與現有的採礦模型互動，以根據 excel 資料表、excel 範圍或另一個資料來源中的資料進行預測。 將新資料套用至現有模型以預測趨勢的程式稱為「*預測查詢*」。  
  
 **查詢**wizard 也會提供一個 [高級編輯器]，用於建立或修改資料採礦模型、產生自訂查詢，或使用其他工具（例如，嵌套資料集）不支援的結構。  
  
-   使用文字編輯器，輸入或貼上您在別處建立的資料採礦延伸模組（DMX）語句。  
  
-   使用互動式查詢產生器，透過範本和對話方塊的協助撰寫自訂 DMX 陳述式。  
  
-   建立 DMX 陳述式以管理或備份採礦模型和結構。  
  
## <a name="using-the-query-wizard"></a>使用查詢精靈  
  
1.  首先，您必須針對要當做輸入使用的資料指定來源。 您可以使用現有 Excel 資料表或範圍中的資料，或者也可以指定 SQL 陳述式來擷取資料。  
  
2.  接下來，此精靈會呈現連接之伺服器上的資料採礦模型清單。 如果您知道您想要的模型，並熟悉資料採礦，您也可以按一下 [ **Advanced** ] 以開啟 [**資料採礦的先進查詢編輯器**]。  
  
3.  根據選擇的模型類型而定，您必須指定包含要評估之資料的資料行，以及定義輸入資料行和模型資料行之間的對應。 根據選擇的演算法而定，您可以設定此模型的其他屬性。  
  
4.  最後，此精靈也會讓您有能力可選擇一或多個預測，以及指定要儲存結果的目的地。  
  
 您隨時都可以按一下 [ **Advanced** ]，切換至 [**資料採礦先進查詢編輯器**]，讓您更充分掌控 DMX 語句的每個部分。 如需如何使用 advanced query 編輯工具的詳細資訊，請參閱[先進資料採礦查詢編輯器](advanced-data-mining-query-editor.md)。  
  
### <a name="requirements"></a>需求  
 若要使用**查詢**嚮導，您必須連接到的實例[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。 此外，此伺服器必須至少包含一個適當類型的資料採礦模型。 如果沒有可用的採礦模型，您可以使用適用於 Excel 的資料採礦用戶端中所提供的精靈來建立採礦模型。 如需如何使用 wizard 建立新的「挖掘模式」的詳細資訊，請參閱[建立資料採礦模型](creating-a-data-mining-model.md)。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;適用于 Excel 的資料採礦增益集部署和調整採礦模型&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)   
 [適用于 Excel &#40;SQL Server 資料採礦增益集的資料採礦用戶端&#41;](data-mining-client-for-excel-sql-server-data-mining-add-ins.md)  
  
  
