---
title: "第 10 課：建立階層 | Microsoft Docs"
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
ms.assetid: 1e2561d3-4890-4495-a9cd-84eb88508938
caps.latest.revision: 23
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 第 10 課：建立階層
在這一課，您將建立階層。 階層是以層級排列的資料行群組；例如，[地理位置] 階層可能有 [國家/地區]、[州省]、[縣市]、[縣 (市)] 的子層級。 在報表用戶端應用程式欄位清單中，階層可以與其他資料行分開顯示，讓用戶端使用者更易於導覽及包含在報表中。 如需詳細資訊，請參閱[ &#40;SSAS 表格式&#41;](../analysis-services/tabular-models/hierarchies-ssas-tabular.md)。  
  
若要建立階層，您將使用 [圖表檢視] 中的模型設計師。 不支援在模型設計師的 [資料檢視] 中建立及管理階層。  
  
完成本課程的估計時間：**20 分鐘**  
  
## 必要條件  
本主題是表格式模型教學課程的一部分，必須依序完成。 在執行本課程的工作之前，您應已完成上一課：[第 9 課：建立檢視方塊](../Topic/Lesson%209:%20Create%20Perspectives.md)。  
  
## 建立階層  
  
#### 在產品資料表中建立類別目錄階層  
  
1.  在模型設計師中，按一下 [模型] 功能表，然後指向 [模型檢視]，再按一下 [圖表檢視]。  
  
  
  
2.  以滑鼠右鍵按一下 [產品] 資料表，然後按一下 [建立階層]。 新的階層會出現在資料表視窗的底部。  
  
3.  在階層名稱中，輸入**類別目錄**來重新命名階層，然後按 ENTER。  
  
4.  在 [產品] 資料表中，按一下 [Product Category Name] 資料行，接著將它拖曳到 [類別目錄] 階層，然後在 [類別目錄] 的頂部放開。  
  
5.  在 [類別目錄] 階層中，以滑鼠右鍵按一下 [Product Category Name] 資料行，然後按一下 [重新命名]，再輸入**類別目錄**。  
  
    > [!NOTE]  
    > 重新命名階層中的資料行並不會重新命名資料表中的該資料行。 階層中的資料行只是資料表中資料行的表示。  
  
6.  在 [產品] 資料表中，按一下並將 [Product Subcategory Name] 資料行拖曳至 [類別目錄] 階層。  
  
7.  將 **Product Subcategory Name** 重新命名為**子類別目錄**。  
  
8.  按照順序按一下並拖曳 [Model Name] 和 [Product Name] 資料行，並將它們放在 [Product Subcategory Name] 資料行下方。 分別將這兩個資料行重新命名為**模型**和**產品**。  
  
#### 在日期資料表中建立階層  
  
1.  在模型設計師中，以滑鼠右鍵按一下 [日期] 資料表，然後按一下 [建立階層]。  
  
2.  將階層重新命名為 **Calendar**。  
  
3.  依序加入下列資料行，然後將它們重新命名：  
  
    |資料行|重新命名為：|  
    |----------|--------------|  
    |Calendar Year|Year|  
    |Calendar Semester|半年度|  
    |Calendar Quarter|Quarter|  
    |Month Calendar|Month|  
    |Day Of Month|Day|  
  
4.  在 [日期] 資料表中重複上述步驟，建立 [Fiscal] 階層，包括下列資料行：  
  
    |資料行|重新命名為：|  
    |----------|--------------|  
    |Fiscal Year|Year|  
    |Fiscal Semester|半年度|  
    |Fiscal Quarter|Quarter|  
    |Month Calendar|Month|  
    |Day Of Month|Day|  
  
5.  最後，在 [日期] 資料表中重複上述步驟，建立 [Production Calendar] 階層，包括下列資料行：  
  
    |資料行|重新命名為：|  
    |----------|--------------|  
    |Calendar Year|Year|  
    |Week Number Of Year|週|  
    |週中的日|Day|  
  
## 後續步驟  
若要繼續進行本教學課程，請前往下一課：[第 11 課：建立資料分割](../analysis-services/lesson-11-create-partitions.md)。  
  
  
  
