---
title: 資料採礦查詢 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataminingquery.f1
ms.assetid: 948e358a-6245-429f-82c7-4cedc5e048fd
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6ab9374312051ab22aa90c48bfed40713fe4e318
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "71298312"
---
# <a name="data-mining-query"></a>資料採礦查詢

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  設計窗格包含資料採礦預測查詢產生器，您可以使用該產生器來建立資料採礦預測查詢。 您可以依據輸入資料表來設計預測查詢，或設計單一預測查詢。 切換到結果檢視以執行查詢並檢視結果。 查詢檢視會顯示預測查詢產生器所建立的資料採礦延伸模組 (DMX) 查詢。  
  
## <a name="options"></a>選項。  
 切換檢視按鈕  
 按一下圖示，即可在設計與查詢窗格之間切換。 預設會開啟設計窗格。  
  
 若要切換到設計窗格，請按一下 ![設計圖示](../../integration-services/control-flow/media/ssis-designicon.gif "設計圖示") 圖示。  
  
 若要切換到查詢窗格，請按一下 ![SQL 圖示](../../integration-services/control-flow/media/ssis-queryicon.gif "SQL 圖示") 圖示。  
  
 **採礦模型**  
 顯示選取的採礦模型，並以此模型作為預測的基礎。  
  
 **選取模型**  
 開啟 [選取採礦模型]  對話方塊。  
  
 **輸入資料行**  
 顯示用來產生預測之選取的輸入資料行。  
  
 **Source**  
 從下拉式清單中，選取包含您將用於資料行之欄位的來源。 您可以使用在 [採礦模型]  資料表中選取的採礦模型、在 [選取輸入資料表]  資料表中選取的輸入資料表、預測函數或自訂運算式。  
  
 可以將資料行從包含採礦模型和輸入資料行的資料表，拖曳至資料格。  
  
 **欄位**  
 從衍生自來源資料表的資料行清單中，選取一個資料行。 如果在 [來源]  中選取 [預測函數]  ，則此資料格會包含選取的採礦模型可用之預測函數的下拉式清單。  
  
 **別名**  
 伺服器所傳回之資料行的名稱。  
  
 **顯示**  
 選取即可傳回資料行或只使用 WHERE 子句中的資料行。  
  
 **群組**  
 配合 [及/或]  資料行，即可將運算式群組在一起。 例如 (expr1 OR expr2) AND expr3。  
  
 **及/或**  
 用於建立邏輯查詢。 例如 (expr1 OR expr2) AND expr3。  
  
 **準則/引數**  
 指定套用至資料行的條件或使用者運算式。 可以將資料行從包含採礦模型和輸入資料行的資料表，拖曳至資料格。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦查詢工具](https://docs.microsoft.com/analysis-services/data-mining/data-mining-query-tools)   
 [資料採礦延伸模組 &#40;DMX&#41; 陳述式參考](../../dmx/data-mining-extensions-dmx-statements.md)  
  
  
