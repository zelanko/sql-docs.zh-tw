---
title: "設定資料流目的地 | Microsoft Docs"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "SQL11.DTS.DESIGNER.DATASTREAMINGDEST.F1"
ms.assetid: bcdbb833-20c8-47ff-a641-bb517f9a1af3
caps.latest.revision: 7
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 7
---
# 設定資料流目的地
  您可以使用 [Advanced Editor for Data Streaming Destination (資料流目的地進階編輯器)] 對話方塊來設定資料流目的地。 若要開啟此對話方塊，請按兩下元件，或在資料流程設計師中，以滑鼠右鍵按一下元件，然後按一下 [編輯]。  
  
 此對話方塊有三個索引標籤︰[元件屬性]、[輸入資料行] 和 [輸入與輸出屬性]。  
  
## [元件屬性] 索引標籤  
 此索引標籤具有以下可以編輯的欄位：  
  
|欄位|說明|  
|-----------|-----------------|  
|名稱|封裝中資料流目的地元件的名稱。|  
|ValidateExternalMetadata|指出元件是否在設計階段就使用外部資料來源驗證。 如果設定為 false，對外部資料來源的驗證會延遲到執行階段。|  
|IDColumnName|[資料摘要發行精靈] 所產生的檢視具有此其他識別碼資料行。 當其他應用程式將資料作為 OData 摘要使用時，識別碼資料行將作為資料流程輸出資料的 EntityKey。<br /><br /> 此資料行的預設名稱是 _ID。 您可以為 ID 資料行指定不同的名稱。|  
  
## 輸入資料行索引標籤  
 在此索引標籤的上方窗格中，您會看到所有可用輸入資料行。 選取您想要在此元件輸出中包含的資料行。 在下方窗格中的清單，會顯示所選資料行。 您可以藉由在清單中輸入 [輸出別名]欄位的新名稱，變更輸出資料行的名稱。  
  
## 輸入與輸出屬性索引標籤  
 類似於 [輸入資料行] 索引標籤，您可以變更此索引標籤中的輸出資料行名稱。 在左側樹狀檢視中，依序展開 [Data Streaming Destination 輸入] 和 [輸入資料行]。 按一下輸入資料行名稱，在右窗格中的輸出資料行名稱中變更名稱。  
  
## 請參閱＜  
 [資料流目的地](../../integration-services/data-flow/data-streaming-destination.md)   
 [逐步解說︰發行 SSIS 封裝做為 SQL 檢視](../../integration-services/data-flow/walkthrough-publish-an-ssis-package-as-a-sql-view.md)  
  
  