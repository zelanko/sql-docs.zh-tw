---
title: "使用 MicrosoftML 封裝與 SQL Server R 服務 | Microsoft Docs"
ms.custom: ""
ms.date: "01/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 1c377717-e281-431e-8171-3924dcce1cdd
caps.latest.revision: 12
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# 使用 MicrosoftML 封裝與 SQL Server R 服務
隨附於 Microsoft R Server 和 SQL Server vNext CTP 1.0 的 **MicrosoftML** 封裝，包含多種 Microsoft 開發的機器學習服務演算法，支援多核心處理和快速資料流。 此封裝也包含文字處理和功能的轉換。

### <a name="new-machine-learning-algorithms"></a>新的機器學習服務演算法


-  **快速線性。** 可用於二元分類或迴歸的推測雙座標堆疊型線性學習工具。 此模型支援 L1 和 L2 正規化。

- **快速的樹狀結構。** 原先稱為 FastRank 的推進式決策樹演算法，為 Bing 開發使用。 它是最快且最受歡迎的學習工具之一。 支援二進位的分類和迴歸。

- **快速樹系。** 以隨機樹系方法為基礎的羅吉斯迴歸模型。 類似於 RevoScaleR 中的 `rxLogit` 函數，但支援 L1 和 L2 正規化。 支援二進位的分類和迴歸。

- **羅吉斯迴歸。** 羅吉斯迴歸模型類似於 RevoScaleR 中的 `rxLogit` 函數，並另外支援 L1 和 L2 正規化。 支援二進位或多級分類。

- **類神經網路。** 二進位分類、多級分類和迴歸的類神經網路模型。 支援 GPU 加速功能和可自訂的迂迴網路。

- **單類別 SVM。** 以 SVM 方法為基礎的異常偵測模型，可用於不對稱資料集的二元分類。

## <a name="transformation-functions"></a>轉換函數

**MicrosoftML** 封裝也包含可用來轉換資料和擷取功能的下列函數。

- `featurizeText()`
 
  在指定的文字字串中，會產生 ngrams 的計數。 

  此函數包括偵測所用語言、執行文字 token 化和正規化、移除停用字詞，以及從文字產生功能的選項。 

- `categorical()`

  建置分類字典，並將每個類別轉換成指標向量。 
 
- `categoricalHash()`

  透過雜湊值及將雜湊用為包中的索引，將類別值轉換成指標陣列。  

- `selectFeatures()` 

  計算非預設值或計算相對於標籤的相互資訊分數，從指定的變數中選取功能子集。 

如需這些新功能的詳細資訊，請參閱 [MicrosoftML functions](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml) (MicrosoftML 函式)。

## <a name="support-for-microsoftml-in-r-services"></a>R 服務的 MicrosoftML 支援

**MicrosoftML** 封裝與 **RevoScaleR** 封裝所使用的資料處理管線完全整合。 目前，任何的 Windows 計算內容中皆可以使用 **MicrosoftML** 封裝，包括 SQL Server R 服務。



## <a name="see-also"></a>另請參閱


[RevoScaleR Functions](https://msdn.microsoft.com/microsoft-r/scaler/scaler) (RevoScaleR 函式)

