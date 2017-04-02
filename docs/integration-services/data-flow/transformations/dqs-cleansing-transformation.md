---
title: "DQS 清理轉換 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "資料連接"
  - "校正資料"
ms.assetid: d2ec1b1a-c745-4741-b57c-6fdb524a154c
caps.latest.revision: 35
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 35
---
# DQS 清理轉換
  DQS 清理轉換會使用 Data Quality Services (DQS) 來更正連接之資料來源的資料，方法是套用針對所連接資料來源或相似資料來源而建立的核准規則。 如需有關資料更正規則的詳細資訊，請參閱＜ [DQS Knowledge Bases and Domains](../../../data-quality-services/dqs-knowledge-bases-and-domains.md)＞。 如需有關 DQS 的詳細資訊，請參閱＜ [Data Quality Services Concepts](../../../data-quality-services/data-quality-services-concepts.md)＞。  
  
 為了判斷資料是否必須更正，DQS 清理轉換會在符合下列條件的情況下，處理來自輸入資料行的資料：  
  
-   已選擇要進行資料更正的資料行。  
  
-   可支援對該資料行的資料類型進行資料更正。  
  
-   資料行對應至具有相容資料類型的定義域。  
  
 轉換還包括您設定來處理資料列層級錯誤的錯誤輸出。 若要設定錯誤輸出，請使用 **[DQS 清理轉換編輯器]**。  
  
 您可以在資料流程中包括 [Fuzzy Grouping Transformation](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md) ，用於識別資料中可能重複的資料列。  
  
## 資料品質專案及值  
 當您使用 DQS 清理轉換處理資料時，會在資料品質伺服器上建立清理專案。 您可以使用 Data Quality Client 管理專案。 此外，您也可以使用 Data Quality Client 將專案值匯入 DQS 知識庫定義域。 您可以只將值匯入設定為使用 DQS 清理轉換的定義域 (或連結的定義域)。  
  
## 相關工作  
  
-   [在 Data Quality Client 中開啟 Integration Services 專案](../../../data-quality-services/open-integration-services-projects-in-data-quality-client.md)  
  
-   [Import Cleansing Project Values into a Domain](../../../data-quality-services/import-cleansing-project-values-into-a-domain.md)  
  
-   [將資料品質規則套用至資料來源](../../../integration-services/data-flow/transformations/apply-data-quality-rules-to-data-source.md)  
  
## 相關內容  
  
-   [開啟、解除鎖定、重新命名和刪除資料品質專案](https://msdn.microsoft.com/library/hh510417.aspx)  
  
-   social.technet.microsoft.com 上的文章： [使用複合定義域清理複雜的資料](http://social.technet.microsoft.com/wiki/contents/articles/13324.using-dqs-cleansing-complex-data-using-composite-domains.aspx)。  
  
  