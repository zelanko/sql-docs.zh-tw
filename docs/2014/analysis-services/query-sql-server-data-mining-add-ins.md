---
title: 查詢 （SQL Server 資料採礦增益集） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- queries [data mining]
- Data Mining Query Advanced Editor
- query builder [data mining]
- DMX
ms.assetid: 16af4a6f-18d4-496a-a304-7a13aa32ee76
caps.latest.revision: 16
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7c2ddae6582355e271488389d6e4005a5d235a74
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37289774"
---
# <a name="query-sql-server-data-mining-add-ins"></a>查詢 (SQL Server 資料採礦增益集)
  ![查詢模型按鈕、 資料採礦功能區](media/dmc-query.gif "查詢模型按鈕、 資料採礦功能區")  
  
 **查詢**精靈可協助您以根據 Excel 資料表、 Excel 範圍或另一個資料來源中的資料進行預測的現有採礦模型互動。 將新的資料套用至現有的模型來預測趨勢的程序稱為*預測查詢*。  
  
 **查詢**精靈也提供了進階的編輯器，建立或修改資料採礦模型、 產生自訂查詢，或使用不支援在其他工具，例如巢狀資料集的結構。  
  
-   使用文字編輯器來輸入或貼入您在其他工具中建立的資料採礦延伸模組 (DMX) 陳述式。  
  
-   使用互動式查詢產生器，透過範本和對話方塊的協助撰寫自訂 DMX 陳述式。  
  
-   建立 DMX 陳述式以管理或備份採礦模型和結構。  
  
## <a name="using-the-query-wizard"></a>使用查詢精靈  
  
1.  首先，您必須針對要當做輸入使用的資料指定來源。 您可以使用現有 Excel 資料表或範圍中的資料，或者也可以指定 SQL 陳述式來擷取資料。  
  
2.  接下來，此精靈會呈現連接之伺服器上的資料採礦模型清單。 如果您知道您想要且不熟悉資料採礦模型時，您也可以按一下**進階**來開啟**資料採礦進階查詢編輯器**。  
  
3.  根據選擇的模型類型而定，您必須指定包含要評估之資料的資料行，以及定義輸入資料行和模型資料行之間的對應。 根據選擇的演算法而定，您可以設定此模型的其他屬性。  
  
4.  最後，此精靈也會讓您有能力可選擇一或多個預測，以及指定要儲存結果的目的地。  
  
 在任何時間，您可以按一下**進階**轉為**資料採礦進階查詢編輯器**，這可讓您更充分掌控每一部分的 DMX 陳述式。 如需如何使用進階的查詢編輯工具的詳細資訊，請參閱[進階資料採礦查詢編輯器](advanced-data-mining-query-editor.md)。  
  
### <a name="requirements"></a>需求  
 若要使用**查詢**精靈，您必須連接到的執行個體[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。 此外，此伺服器必須至少包含一個適當類型的資料採礦模型。 如果沒有可用的採礦模型，您可以使用適用於 Excel 的資料採礦用戶端中所提供的精靈來建立採礦模型。 如需有關如何使用精靈建立新的採礦模型的資訊，請參閱 <<c0> [ 建立資料採礦模型](creating-a-data-mining-model.md)。  
  
## <a name="see-also"></a>另請參閱  
 [部署及調整採礦模型&#40;資料採礦適用於 Excel 的增益集&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)   
 [適用於 Excel 的資料採礦用戶端&#40;SQL Server 資料採礦增益集&#41;](data-mining-client-for-excel-sql-server-data-mining-add-ins.md)  
  
  
