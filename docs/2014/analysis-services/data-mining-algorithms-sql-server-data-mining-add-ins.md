---
title: 資料採礦演算法（SQL Server 資料採礦增益集） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- segmentation
- data mining algorithms
- clustering [data mining]
- linear regression
- association [data mining]
- neural networks
- logistic regression
- regression
- sequence analysis
- decision tree [data mining]
- Naive Bayes
- time series [data mining]
ms.assetid: 3a1a62e4-9fb5-4cdb-a6c6-1b8b30d417ef
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6e0bf6c0c1126dff29107636e0956d92d4b314a7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66086505"
---
# <a name="data-mining-algorithms-sql-server-data-mining-add-ins"></a>資料採礦演算法 (SQL Server 資料採礦增益集)
  適用於 Office 的資料採礦增益集支援使用下列資料採礦演算法建立分析模型。 所有的演算法都是根據已知的機器學習方法而由 Microsoft Research 實作過。  
  
## <a name="algorithms"></a>演算法  
  
|機器學習方法|運作方式|  
|-----------------------------|------------------|  
|Microsoft 關聯規則演算法|探索會一起購買的產品或一同發生的事件，並且使用模型產生建議。<br /><br /> [https://msdn.microsoft.com/library/ms174916.aspx](https://msdn.microsoft.com/library/ms174916.aspx)|  
|Microsoft 叢集演算法|定義市場區隔、自動將相關的客戶分組，或尋找資料的關聯性以用於進一步採礦。<br /><br /> [https://msdn.microsoft.com/library/ms174879.aspx](https://msdn.microsoft.com/library/ms174879.aspx)|  
|Microsoft 決策樹演算法|識別資料的各種元素之間原本未知的關聯性，以利做出更明智的決策或尋找導致特定結果的因素。<br /><br /> [https://msdn.microsoft.com/library/ms174923.aspx](https://msdn.microsoft.com/library/ms174923.aspx)|  
|Microsoft 線性迴歸演算法|尋找數學公式，其內容描述促成數值結果的因素。<br /><br /> [https://msdn.microsoft.com/library/ms174824.aspx](https://msdn.microsoft.com/library/ms174824.aspx)|  
|Microsoft 羅吉斯迴歸演算法|識別促成二進位結果的因素，並且學習如何運用這些因素來影響結果。<br /><br /> [https://msdn.microsoft.com/library/ms174828.aspx](https://msdn.microsoft.com/library/ms174828.aspx)|  
|Microsoft 貝氏機率分類演算法|探索資料的關聯性，並且尋找與特定結果最密切相關的關聯性。<br /><br /> [https://msdn.microsoft.com/library/ms174806.aspx](https://msdn.microsoft.com/library/ms174806.aspx)|  
|Microsoft 類神經網路演算法|尋找多項輸入甚至多項輸出之間隱藏的關聯性。 用於進行探索或預測。<br /><br /> [https://msdn.microsoft.com/library/ms174941.aspx](https://msdn.microsoft.com/library/ms174941.aspx)|  
|Microsoft 時間序列演算法|使用歷程記錄資料預測未來值。<br /><br /> [https://msdn.microsoft.com/library/ms174923.aspx](https://msdn.microsoft.com/library/ms174923.aspx)|  
  
## <a name="advanced-options"></a>進階選項  
 當您使用適用於 Excel 的資料採礦用戶端時，您可以選擇建立自己的資料採礦結構和模型或是微調演算法的參數。  
  
 [SQL Server 資料採礦增益集 &#40;的演算法參數&#41;](algorithm-parameters-sql-server-data-mining-add-ins.md)  
  
 使用這些進階選項自訂模型的方式有兩種：  
  
-   使用 **[資料採礦查詢]** 精靈建立模型。  
  
-   在 **[資料採礦用戶端]** 中啟動精靈之後，按一下 **[參數]**。  
  
## <a name="see-also"></a>另請參閱  
 [查詢 &#40;SQL Server 資料採礦增益集&#41;](query-sql-server-data-mining-add-ins.md)   
 [適用于 Excel&#41;的先進模型化 &#40;資料採礦增益集](advanced-modeling-data-mining-add-ins-for-excel.md)  
  
  
