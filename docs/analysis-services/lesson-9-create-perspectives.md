---
title: "第 9 課：建立檢視方塊 | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 55b0f0d0-1cdf-4876-9c3d-d0c848be3f5d
caps.latest.revision: 23
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 第 9 課：建立檢視方塊
在這一課，您將建立一個 [網際網路銷售] 檢視方塊。 檢視方塊會定義可檢視之模型的子集，而這類子集會提供有焦點的商務特有或應用程式特有視點。 使用者使用檢視方塊連接到模型時，只會將那些模型物件 (資料表、資料行、量值、階層和 KPI) 視為該檢視方塊中定義的欄位。  
  
您在本課中所建立的網際網路銷售額檢視方塊將不包含 Customer 資料表物件。 當您建立從檢視表中排除某些物件的檢視方塊時，該物件仍然會存在於模型中，但是在報表用戶端欄位清單中看不到。 導出資料行嗨量值無論是否包含在檢視方塊中，都仍然可以從遭排除之物件資料中計算。  
  
本課程的目的在於描述如何建立檢視方塊，以及熟悉表格式模型撰寫工具。 如果您之後展開此模型納入其他資料表，可以建立其他檢視方塊來定義不同的模型視點，例如存貨和銷售人員。  
  
如需詳細資訊，請參閱[檢視方塊 &#40;SSAS 表格式&#41;](../analysis-services/tabular-models/perspectives-ssas-tabular.md)。  
  
完成本課程的估計時間：**5 分鐘**  
  
## 必要條件  
本主題是表格式模型教學課程的一部分，必須依序完成。 在執行本課中的工作之前，您應已完成上一課：[第 8 課：建立關鍵效能指標](../analysis-services/lesson-8-create-key-performance-indicators.md)。  
  
## 建立檢視方塊  
  
#### 若要建立網際網路銷售檢視方塊  
  
1.  在模型設計師中，依序按一下 [模型] 功能表、[檢視方塊] 和 [建立及管理]。  
  
2.  在 [檢視方塊] 對話方塊中，按一下 [新增檢視方塊]。  
  
3.  若要重新命名檢視方塊，請按兩下 [新的檢視方塊 1] 欄名，然後輸入**網際網路銷售**。  
  
4.  在 [欄位] 中，選取下列資料表：[Date]、[Geography]、[Product]、[Product Category]、[Product Subcategory] 和 [Internet Sales]。  
  
    請注意，您從此檢視方塊中排除了 Customer 資料表及其所有資料行。 稍後，您將在第 12 課中使用 [在 Excel 中進行分析] 功能測試此檢視方塊。 Excel 樞紐分析表欄位清單將包含 Customer 資料表之外的每個資料表。  
  
5.  驗證您所做的選擇，確定未核取 [Customer] 資料表，然後按一下 [確定]  
  
## 後續步驟  
若要繼續進行本教學課程，請前往下一課：[第 10 課：建立階層](../analysis-services/lesson-10-create-hierarchies.md)。  
  
  
  
