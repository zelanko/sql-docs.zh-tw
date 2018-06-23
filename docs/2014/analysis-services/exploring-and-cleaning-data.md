---
title: 瀏覽和清除資料 |Microsoft 文件
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7c888c95-8986-461e-9f11-2395044b9d97
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 0c39eaa58152fd1a75eeaefdc79bae93ccd36b98
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023245"
---
# <a name="exploring-and-cleaning-data"></a>瀏覽和清除資料
  資料準備不只是進行資料清理而已。 務必記得，準備資料的方式也會影響最後解譯結果的方式。 資料準備包含下列工作：  
  
-   瀏覽及檢查資料分佈情形。  
  
-   清除不正確的記錄，以及選擇要進行資料採礦的資料行。  
  
-   適當處理 Null。  
  
-   分類收納值，或依不同的時段彙總值。  
  
-   加入標籤來改善結果的可用性。  
  
-   視需要轉換資料類型或將值分類以進行分析。  
  
 如果您不熟悉資料模型化，我們建議您閱讀相關的主題: <<c0> [ 檢查清單的資料採礦準備](checklist-of-preparation-for-data-mining.md)。  
  
## <a name="data-preparation-tools"></a>資料準備工具  
 適用於 Office 的資料採礦增益集包括了可用於資料清理和準備的以下工具：  
  
### <a name="explore-data"></a>瀏覽資料  
 使用**瀏覽資料**精靈進行這些資料準備工作：  
  
-   預覽資料並識別出必須在分析之前修正的錯誤。  
  
-   收集統計資訊，有助於了解資料的平衡與必要的清除工作。  
  
-   識別對分析有用的資料行，並規劃資料模型化階段。  
  
 [瀏覽資料&#40;SQL Server 資料採礦增益集&#41;](explore-data-sql-server-data-mining-add-ins.md)。  
  
### <a name="detect-and-handle-outliers"></a>偵測及處理極端值  
 **極端值**精靈圖形中值分佈的資料，並幫助您移除極端值。 使用**極端值**工具進行下列資料準備工作：  
  
-   根據在資料中找到的模式來判斷個別值是否可靠。  
  
-   檢閱不尋常的值並採取行動來刪除或取代它們。  
  
-   將模型限定在某指定範圍的值。 例如，如果您知道某特定商店有極端值，您可以刪除該值並取得更能準確預測其他商店的模型。  
  
 [極端值&#40;SQL Server 資料採礦增益集&#41;](outliers-sql-server-data-mining-add-ins.md)。  
  
### <a name="relabel-and-bin-data"></a>重定標籤和分類收納資料  
 **重定標籤**精靈分組的資料值，因此您可以變更索引標籤上的資料。 使用重定標籤工具來進行以下這些資料準備工作：  
  
-   將調查結果中使用的數字代碼變更為此數字代碼所代表的文字描述。  
  
     例如，您可以取代資料項目 (例如以 Gender = Female 取代 Gender = 1)。  
  
-   您可以建立代表數量範圍的群組，來分類收納資料。  
  
     比方說，您可能想要收入 資料行的數字取代標籤例如**收入 – 中度**和**收入-高**。  
  
-   將離散值摺疊成類別目錄。  
  
     例如，如果您有太多個別產品偵測到購買模式，您可以嘗試將這些產品指派到更廣泛的類別目錄。  
  
 [重定標籤&#40;SQL Server 資料採礦增益集&#41;](relabel-sql-server-data-mining-add-ins.md)  
  
### <a name="cleanse-data"></a>清理資料  
 資料清理包含各種活動，大部分活動由增益集支援。  
  
-   識別 Null 值，並判斷是否應該將這些值變更為實數值，或視為 `Missing` 值來處理。  
  
-   偵測遺漏的值，然後移除它們或推算一個適當的值，例如平均值、Null 或其他值。  
  
 [瀏覽資料&#40;SQL Server 資料採礦增益集&#41;](explore-data-sql-server-data-mining-add-ins.md)  
  
 [重定標籤&#40;SQL Server 資料採礦增益集&#41;](relabel-sql-server-data-mining-add-ins.md)  
  
 [根據範例填滿](fill-from-example-table-analysis-tools-for-excel.md)  
  
### <a name="sample-data"></a>取樣資料  
 取樣資料精靈提供兩種方法，可用來建立定型模型和測試模型的對稱資料集。  
  
-   **隨機取樣。** 使用這個選項即可從較大資料集擷取代表性資料集，以用於定型或測試。 資料採礦增益集使用*分層取樣*以確保組平衡的值取得每個取樣的變數。  
  
-   **超取樣。** 當您的資料比目標結果所需的資料少，而必須提高資料的加權時，請使用這個選項。 例如，詐欺可能相當罕見，不過您可以超取樣與詐欺相關的案例，為模型取得足夠的資料。  
  
 [範例資料&#40;SQL Server 資料採礦增益集&#41;](sample-data-sql-server-data-mining-add-ins.md)。  
  
## <a name="see-also"></a>另請參閱  
 [建立資料採礦模型](creating-a-data-mining-model.md)   
 [驗證模型及使用模型進行預測&#40;資料採礦 excel 增益集&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)   
 [部署及調整採礦模型&#40;資料採礦 excel 增益集&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  