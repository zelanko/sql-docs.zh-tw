---
title: 儲存資料採礦查詢結果對話方塊 （採礦模型預測檢視） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dm.savedataminingqueryresult.f1
helpviewer_keywords:
- Save Data Mining Query Result dialog box
ms.assetid: 112fb527-7466-4fd4-9cf1-75596135648f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c4736083dedc6899a55e49926d1010ef39fc4444
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48090271"
---
# <a name="save-data-mining-query-result-dialog-box-mining-model-prediction-view"></a>儲存資料採礦查詢結果對話方塊 (採礦模型預測檢視)
  使用 **[儲存資料採礦查詢結果]** 對話方塊，即可將資料採礦查詢的結果儲存到新的資料表。  
  
 新的資料表將建立在資料來源所定義的資料庫中。  
  
## <a name="options"></a>選項。  
 **資料來源**  
 從目前的專案中選取資料來源。 如果正確的資料來源不存在，請按一下 **[新增]** 建立新的資料來源。  
  
 **新增**  
 開啟 [資料來源精靈]。  
  
 **資料表名稱**  
 輸入新資料表的名稱。  
  
 **如果覆寫存在**  
 如果您要以相同名稱覆寫現有的資料表，請選取此選項。  
  
 如果下列任何一種情況成立，就必須覆寫現有的資料表：  
  
-   您已將資料行加入至預測查詢。  
  
-   您已在預測查詢中變更任何資料行的名稱或資料類型。  
  
-   您已在目的地資料表上執行 ALTER 陳述式。  
  
 如果多個資料行具有相同的名稱 (例如，許多衍生的資料行可能具有預設資料行名稱 [運算式])，您就必須針對名稱重複的每個資料行建立別名。 如果資料行沒有唯一的名稱，當設計師嘗試將結果儲存至 SQL Server 時，將會引發錯誤，因為資料表中的資料行必須具有唯一的名稱。  
  
 **加入至 DSV**  
 (選擇性) 如果您要將資料表加入至現有的資料來源，請選取專案中包含的資料來源檢視。  
  
 如果您想要在相同的資料來源中保留模型的所有相關資料表 (例如定型資料、預測來源資料和查詢結果)，這個選項就很有用。  
  
## <a name="see-also"></a>另請參閱  
 [預測查詢產生器&#40;資料採礦&#41;](prediction-query-builder-data-mining.md)   
 [資料採礦查詢介面](data-mining/data-mining-query-tools.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 陳述式參考](/sql/dmx/data-mining-extensions-dmx-statements)  
  
  
