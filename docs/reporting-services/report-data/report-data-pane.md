---
title: "報表資料窗格 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "10039"
  - "sql13.rtp.rptdesigner.reportdata.f1"
  - "10435"
helpviewer_keywords: 
  - "報表資料窗格"
ms.assetid: aa9614a3-12e7-4e17-9de2-fafccd1f5f9d
caps.latest.revision: 28
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 28
---
# 報表資料窗格
  [報表資料] 窗格可用於檢視報表中目前定義的參數、資料來源、資料集、欄位集合和影像。 [圖表資料] 會以階層檢視來顯示表示報表中資料的項目。 最上層節點代表內建欄位、參數、影像和資料來源參考。 請展開每個節點以檢視資料項目。 例如，當您展開資料來源節點時，為該資料來源所定義的資料集就會顯示。 在展開資料集時，其欄位集合就會顯示。 將項目拖曳到報表設計介面，以將資料連結到報表頁面的報表項目。  
  
## 選項。  
 **內建欄位**  
 代表 Reporting Services 所提供的欄位，這些欄位常用於報表中，例如報表名稱或頁碼。 如需詳細資訊，請參閱[運算式中的內建集合 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder-and-ssrs.md)。  
  
 **參數**  
 代表報表參數的集合，每個參數都可以是單一數值或多重值。 如需詳細資訊，請參閱[報表參數 &#40;報表產生器和報表設計師&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)。  
  
 **影像**  
 代表用於報表中的一組影像。 如需詳細資訊，請參閱[影像 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md)。  
  
 **資料來源**  
 代表內嵌資料來源或共用資料來源的單一資料來源參考。 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，共用資料來源會出現在方案總管的 [共用資料來源] 資料夾下方。 資料來源指定 Reporting Services 所支援的資料來源類型之一。 資料來源是以其為基礎之資料集集合的父節點。 如需詳細資訊，請參閱[資料連接、資料來源及連接字串 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)。  
  
 **資料集**  
 代表單一資料集。 資料集是由查詢所指定之欄位集合的父節點，包含任何導出欄位。 Reporting Services 支援查詢設計工具，可協助您指定查詢。 如需詳細資訊，請參閱[報表資料集 &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md) 和[查詢設計工具 &#40;SSRS&#41;](../../reporting-services/report-data/query-design-tools-ssrs.md)。  
  
## 請參閱＜  
 [資料集 Fields 集合 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [群組窗格](../../reporting-services/tools/grouping-pane.md)  
  
  