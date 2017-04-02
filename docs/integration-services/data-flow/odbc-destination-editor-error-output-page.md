---
title: "ODBC 目的地編輯器 (錯誤輸出頁面) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.designer.odbcdest.errorhandling.f1"
ms.assetid: 0a743f8d-2a51-4296-9976-8104f5ca22d3
caps.latest.revision: 7
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 7
---
# ODBC 目的地編輯器 (錯誤輸出頁面)
  使用 **[ODBC 目的地編輯器]** 對話方塊的 **[錯誤輸出]** 頁面，即可選取錯誤處理選項。  
  
 若要了解有關 ODBC 目的地的詳細資訊，請參閱＜ [ODBC Destination](../../integration-services/data-flow/odbc-destination.md)＞。  
  
 **若要開啟 ODBC 目的地編輯器的錯誤輸出頁面**  
  
## 工作清單  
  
-   在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，開啟具有 ODBC 目的地的 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 封裝。  
  
-   在 [資料流程] 索引標籤中，按兩下 ODBC 目的地。  
  
-   在 **[ODBC 目的地編輯器]**中，按一下 **[錯誤輸出]**。  
  
## 選項。  
  
### 輸入/輸出  
 檢視資料來源的名稱。  
  
### 資料行  
 未使用。  
  
### 錯誤  
 選取 ODBC 目的地應該如何處理流程中的錯誤：忽略失敗、重新導向資料列，或使元件失效。  
  
### 截斷  
 選取 ODBC 目的地應該如何處理流程中的截斷：忽略失敗、重新導向資料列，或使元件失效。  
  
### 說明  
 檢視錯誤的描述。  
  
### 將這個值設定到選取的資料格  
 選取發生錯誤或截斷時 ODBC 目的地如何處理所有選取的資料格：忽略失敗、重新導向資料列，或使元件失效。  
  
### 套用  
 將錯誤處理選項套用至選取的資料格。  
  
## 錯誤處理選項  
 您可以使用下列選項來設定 ODBC 目的地處理錯誤和截斷的方式。  
  
### 失敗元件  
 當發生錯誤或截斷時，資料流程工作將失敗。 這是預設行為。  
  
### 忽略失敗  
 忽略錯誤或截斷。  
  
### 重新導向流程  
 導致錯誤或截斷的資料列會導向至 ODBC 目的地的錯誤輸出。 如需詳細資訊，請參閱＜ODBC 目的地＞。  
  
## 請參閱＜  
 [ODBC 目的地編輯器 &#40;連線管理員頁面&#41;](../../integration-services/data-flow/odbc-destination-editor-connection-manager-page.md)   
 [ODBC 目的地編輯器 &#40;對應頁面&#41;](../../integration-services/data-flow/odbc-destination-editor-mappings-page.md)  
  
  