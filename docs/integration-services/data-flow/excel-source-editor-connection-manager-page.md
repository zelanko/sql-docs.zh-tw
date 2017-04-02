---
title: "Excel 來源編輯器 (連接管理員頁面) | Microsoft Docs"
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
  - "sql13.dts.designer.excelsourceadapter.connection.f1"
helpviewer_keywords: 
  - "Excel 來源編輯器"
ms.assetid: 428e04e0-ad98-45d0-8345-12ec1b67b2eb
caps.latest.revision: 39
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 39
---
# Excel 來源編輯器 (連接管理員頁面)
  使用 **[Excel 來源編輯器]** 對話方塊的 **[連接管理員]** 節點，以選取來源要使用的 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 活頁簿。 Excel 來源會從工作表或現有活頁簿的具名範圍中讀取資料。  
  
> [!NOTE]  
>  在 **[Excel 來源編輯器]** 中無法使用 Excel 來源的 **CommandTimeout**屬性，但可使用 **[進階編輯器]**來設定這個屬性。 如需有關這個屬性的詳細資訊，請參閱＜ [Excel Custom Properties](../../integration-services/data-flow/excel-custom-properties.md)＞的＜Excel 來源＞一節。  
  
 若要深入了解 Excel 來源，請參閱＜ [Excel Source](../../integration-services/data-flow/excel-source.md)＞。  
  
## 靜態選項  
 **OLE DB 連接管理員**  
 從清單中選取現有的 Excel 連接管理員，或按一下 [新增] 建立新的連接管理員。  
  
 **新增**  
 使用 [Excel 連接管理員] 對話方塊來建立新的連接管理員。  
  
 **資料存取模式**  
 從來源中指定選取資料的方法。  
  
|Value|說明|  
|-----------|-----------------|  
|資料表或檢視|從工作表或 Excel 檔案的具名範圍中擷取資料。|  
|資料表名稱或檢視名稱變數|在變數中指定工作表或範圍名稱。<br /><br /> **相關資訊︰**[在封裝中使用變數](../Topic/Use%20Variables%20in%20Packages.md)|  
|SQL (命令)|使用 SQL 查詢從 Excel 檔案中擷取資料。 如需有關查詢語法的詳細資訊，請參閱＜ [Excel Source](../../integration-services/data-flow/excel-source.md)＞。|  
|來自變數的 SQL 命令|在變數中指定 SQL 查詢文字。|  
  
 **預覽**  
 使用 [資料檢視] 對話方塊來預覽結果。 預覽最多可顯示 200 個資料列。  
  
## 資料存取模式動態選項  
  
### 資料存取模式 = 資料表或檢視  
 **Excel 工作表的名稱**  
 從 Excel 活頁簿的可用工作表或具名範圍清單中，選取工作表或具名範圍的名稱。  
  
### 資料存取模式 = 資料表名稱或檢視名稱變數  
 **變數名稱**  
 選取包含工作表名稱或具名範圍的變數。  
  
### 資料存取模式 = SQL 命令  
 **SQL 命令文字**  
 輸入 SQL 查詢的文字，按一下 [建立查詢] 建立查詢，或按一下 [瀏覽] 瀏覽至包含查詢文字的檔案。  
  
 **參數**  
 如果您所輸入的參數化查詢使用 ? 做為查詢文字中的參數預留位置，請使用 **[設定查詢參數]** 對話方塊，將查詢輸入參數對應到封裝變數。  
  
 **建立查詢**  
 使用 [查詢產生器] 對話方塊，以視覺化的方式來建構 SQL 查詢。  
  
 **瀏覽**  
 使用 [開啟] 對話方塊來找出包含 SQL 查詢文字的檔案。  
  
 **剖析查詢**  
 請確認查詢文字的語法。  
  
### 資料存取模式 = 來自變數的 SQL 命令  
 **變數名稱**  
 選取包含 SQL 查詢文字的變數。  
  
## 請參閱＜  
 [Integration Services 錯誤和訊息參考](../../integration-services/integration-services-error-and-message-reference.md)   
 [Excel 來源編輯器 &#40;資料行頁面&#41;](../../integration-services/data-flow/excel-source-editor-columns-page.md)   
 [Excel 來源編輯器 &#40;錯誤輸出頁面&#41;](../../integration-services/data-flow/excel-source-editor-error-output-page.md)   
 [Excel 連接管理員](../../integration-services/connection-manager/excel-connection-manager.md)   
 [使用 Foreach 迴圈容器來循環使用 Excel 檔案和資料表](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
  