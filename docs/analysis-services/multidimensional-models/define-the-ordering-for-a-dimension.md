---
title: "定義維度的排序方式 | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "OrderBy 屬性"
  - "維度 [Analysis Services], 排序"
  - "商務智慧增強功能 [Analysis Services], 排序"
  - "維度 [Analysis Services], 商業智慧增強功能"
  - "排序維度 [Analysis Services]"
  - "OrderByAttributeID 屬性"
ms.assetid: c42fbd58-244d-4e0a-b715-6f919cbc3ad9
caps.latest.revision: 31
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 定義維度的排序方式
  將屬性排序方式增強功能加入至 Cube 或維度，即可指定如何排序屬性的成員。 您可以依名稱或屬性的索引鍵來排序成員，或是依名稱或另一個屬性 (根據屬性關聯性) 的索引鍵來排序成員。 依預設，會依名稱來排序成員。 這項增強功能會在維度中變更屬性的 **OrderBy** 和 **OrderByAttributeID** 屬性設定。  
  
 若要加入屬性排序，您可使用 [商業智慧精靈]，並於 [選擇增強功能] 頁面上選取 [指定屬性排列方式] 選項。 然後，此精靈會引導您逐步完成選取要套用屬性排序方式的維度，並指定如何為選取的維度排序屬性。  
  
## 選取維度  
 在精靈的第一個 [指定屬性排列方式] 頁面上，您指定要套用屬性排列方式的維度。 加入到此選取維度的屬性排列方式增強功能，會造成維度的變更。 包含選取之維度的所有 Cube，都會繼承這些變更。  
  
## 指定排列方式  
 在精靈的第二個 [指定屬性排列方式] 頁面上，您指定如何排序維度中的所有屬性。  
  
 在 [排序屬性] 資料行中，您可變更用於執行排序的屬性。 如果您要用來排序成員的屬性不在清單中，請向下捲動清單，然後選取 [\< 新增屬性...>] 以開啟 [選取資料行] 對話方塊，在其中您可選取維度資料表內的資料行。 使用 [選取資料行] 對話方塊選取資料行會建立一個額外的屬性，可用它來排序屬性的成員。  
  
 在 [準則] 資料行中，您可選取要依 [索引鍵] 或 [名稱] 來排序屬性的成員。  
  
  