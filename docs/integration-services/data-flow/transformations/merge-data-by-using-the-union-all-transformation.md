---
title: "使用聯集全部轉換來合併資料 | Microsoft Docs"
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
  - "合併資料集 [Integration Services]"
  - "合併輸入 [Integration Services]"
  - "組合資料集"
  - "聯集全部轉換"
  - "資料集 [Integration Services], 合併"
ms.assetid: 78304403-a81c-4101-b87e-ec80ddfdac98
caps.latest.revision: 22
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 22
---
# 使用聯集全部轉換來合併資料
  若要加入及設定「聯集全部」轉換，封裝必須已包括至少一個「資料流程」工作與兩個資料來源。  
  
 「聯集全部」轉換可合併多個輸入。 連接到轉換的第一個輸入為參考輸入，隨後連接的輸入為次要輸入。 輸出包括參考輸入中的資料行。  
  
### 將輸入合併於資料流程  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 中，按兩下方案總管中的封裝，以在 [[!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師] 中開啟封裝，然後按一下 [資料流程] 索引標籤。  
  
2.  將「聯集全部」轉換從 [工具箱] 拖曳至 [資料流程] 索引標籤的設計介面。  
  
3.  將連接子從資料來源或前一個轉換拖曳至「聯集全部」轉換，以便將「聯集全部」轉換連接到資料流程。  
  
4.  按兩下 [聯集全部] 轉換。  
  
5.  在 [聯集全部轉換編輯器] 中，藉由按一下資料列並選取輸入清單中的資料行，將輸入的資料行對應至 [輸出資料行名稱] 清單中的資料行。 選取輸入清單中的 [\<忽略>]，以略過資料行的對應。  
  
    > [!NOTE]  
    >  兩個資料行之間的對應，會要求資料行的中繼資料相符。  
  
    > [!NOTE]  
    >  未對應至參考資料行之次要輸入中的資料行，在輸出中會設為 Null 值。  
  
6.  (選擇性) 在 [輸出資料行名稱] 資料行中修改資料行的名稱。  
  
7.  針對每個輸入中的每個資料行重複步驟 5 與 6。  
  
8.  按一下 **[確定]**。  
  
9. 若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
## 請參閱＜  
 [聯集全部轉換](../../../integration-services/data-flow/transformations/union-all-transformation.md)   
 [Integration Services 轉換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services 路徑](../../../integration-services/data-flow/integration-services-paths.md)   
 [資料流程工作](../../../integration-services/control-flow/data-flow-task.md)  
  
  