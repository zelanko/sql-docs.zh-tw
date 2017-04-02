---
title: "Excel 目的地編輯器 (連接管理員頁面) | Microsoft Docs"
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
  - "sql13.dts.designer.exceldestadapter.connection.f1"
helpviewer_keywords: 
  - "Excel 目的地編輯器"
ms.assetid: fc13f725-963c-488e-91e2-20627133e842
caps.latest.revision: 43
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 43
---
# Excel 目的地編輯器 (連接管理員頁面)
  使用 **[Excel 目的地編輯器]** 對話方塊的 **[連接管理員]** 頁面，來指定資料來源資訊，以及預覽結果。 Excel 目的地會將資料載入 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 活頁簿中的工作表或具名範圍。  
  
> [!NOTE]  
>  在 **[Excel 目的地編輯器]** 中無法使用 Excel 目的地的 **CommandTimeout**屬性，但可使用 **[進階編輯器]**來設定這個屬性。 此外， **[進階編輯器]**中只會有特定的快速載入選項。 如需有關這個屬性的詳細資訊，請參閱＜ [Excel Custom Properties](../../integration-services/data-flow/excel-custom-properties.md)＞的＜Excel 目的地＞一節。  
  
 若要深入了解 Excel 目的地，請參閱＜ [Excel Destination](../../integration-services/data-flow/excel-destination.md)＞。  
  
## 靜態選項  
 **Excel 連接管理員**  
 從清單中選取現有的 Excel 連線管理員，或按一下 [新增] 建立新的連線管理員。  
  
 **新增**  
 使用 [Excel 連線管理員] 對話方塊來建立新的連線管理員。  
  
 **資料存取模式**  
 從來源中指定選取資料的方法。  
  
|選項|說明|  
|------------|-----------------|  
|資料表或檢視|將資料載入 Excel 資料來源中的工作表或具名範圍。|  
|資料表名稱或檢視名稱變數|在變數中指定工作表或範圍名稱。<br /><br /> **相關資訊：**[在封裝中使用變數](../Topic/Use%20Variables%20in%20Packages.md)|  
|SQL (命令)|使用 SQL 查詢將資料載入 Excel 目的地。|  
  
 **Excel 工作表的名稱**  
 從下拉式清單中選取 Excel 目的地。 如果此清單為空，請按一下 **[新增]**。  
  
 **新增**  
 按一下 [新增] 以啟動 [建立工資料表] 對話方塊。 按一下 **[確定]**時，對話方塊會建立 **[Excel 連接管理員]** 指向的 Excel 檔案。  
  
 **檢視現有的資料**  
 使用 [預覽查詢結果] 對話方塊來預覽結果。 預覽最多可顯示 200 個資料列。  
  
> [!WARNING]  
>  如果您選取的 [Excel 連線管理員] 指向不存在的 Excel 檔，則在您按一下此按鈕時將看到一條錯誤消息。  
  
## 資料存取模式動態選項  
  
### 資料存取模式 = 資料表或檢視  
 **Excel 工作表的名稱**  
 從資料來源裡可用的資訊清單中，選取工作表或具名範圍的名稱。  
  
### 資料存取模式 = 資料表名稱或檢視名稱變數  
 **變數名稱**  
 選取包含工作表名稱或具名範圍的變數。  
  
### 資料存取模式 = SQL 命令  
 **SQL 命令文字**  
 輸入 SQL 查詢的文字，按一下 [建立查詢] 來建立查詢，或是按一下 [瀏覽] 以找出包含查詢文字的檔案。  
  
 **建立查詢**  
 使用 [查詢產生器] 對話方塊，以視覺化的方式來建構 SQL 查詢。  
  
 **瀏覽**  
 使用 [開啟] 對話方塊來找出包含 SQL 查詢文字的檔案。  
  
 **剖析查詢**  
 請確認查詢文字的語法。  
  
## 請參閱＜  
 [Integration Services 錯誤和訊息參考](../../integration-services/integration-services-error-and-message-reference.md)   
 [Excel 目的地編輯器 &#40;對應頁面&#41;](../../integration-services/data-flow/excel-destination-editor-mappings-page.md)   
 [Excel 目的地編輯器 &#40;錯誤輸出頁面&#41;](../../integration-services/data-flow/excel-destination-editor-error-output-page.md)   
 [使用 Foreach 迴圈容器來循環使用 Excel 檔案和資料表](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
  