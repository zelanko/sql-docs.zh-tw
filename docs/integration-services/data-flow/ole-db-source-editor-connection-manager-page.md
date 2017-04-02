---
title: "OLE DB 來源編輯器 (連接管理員頁面) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.oledbsourceadapter.connection.f1"
helpviewer_keywords: 
  - "OLE DB 來源編輯器"
ms.assetid: 53699902-8699-4547-b56b-a5b2079e98b6
caps.latest.revision: 42
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 42
---
# OLE DB 來源編輯器 (連接管理員頁面)
  使用 [OLE DB 來源編輯器] 對話方塊的 [連接管理員] 頁面，來選取來源的 OLE DB 連接管理員。 這個頁面也可以讓您從資料庫中選取資料表或檢視。  
  
> [!NOTE]  
>  若要從使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007 的資料來源載入資料，請使用 OLE DB 來源。 您無法使用 Excel 來源，從 Excel 2007 資料來源載入資料。 如需詳細資訊，請參閱[設定 OLE DB 連接管理員](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)。  
>   
>  若要從使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2003 或更早版本的資料來源載入資料，請使用 Excel 來源。 如需詳細資訊，請參閱 [Excel 來源編輯器 &#40;連接管理員頁面&#41;](../../integration-services/data-flow/excel-source-editor-connection-manager-page.md)。  
  
> [!NOTE]  
>  在 OLE DB 來源編輯器中無法使用 OLE DB 來源的 **CommandTimeout** 屬性，但可使用進階編輯器來設定這個屬性。 如需這個屬性的詳細資訊，請參閱 [OLE DB 自訂屬性](../../integration-services/data-flow/ole-db-custom-properties.md)的＜Excel 來源＞一節。  
  
 若要深入了解 OLE DB 來源，請參閱＜ [OLE DB Source](../../integration-services/data-flow/ole-db-source.md)＞。  
  
## 開啟 OLE DB 來源編輯器 (連接管理員頁面)  
  
1.  將 OLE DB 來源加入 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝 (於 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中)。  
  
2.  以滑鼠右鍵按一下來源元件，然後按一下 [編輯]。  
  
3.  按一下 [連接管理員]。  
  
## 靜態選項  
 **OLE DB 連接管理員**  
 從清單中選取現有的連接管理員，或按一下 [新增] 來建立新的連接。  
  
 **新增**  
 使用 [設定 OLE DB 連接管理員] 對話方塊建立新的連接管理員。  
  
 **資料存取模式**  
 從來源中指定選取資料的方法。  
  
|選項|說明|  
|------------|-----------------|  
|資料表或檢視|從 OLE DB 資料來源中的資料表或檢視擷取資料。|  
|資料表名稱或檢視名稱變數|請在變數中指定資料表或檢視名稱。<br /><br /> **相關資訊︰**[在封裝中使用變數](../Topic/Use%20Variables%20in%20Packages.md)|  
|SQL (命令)|使用 SQL 查詢從 OLE DB 資料來源中擷取資料。|  
|來自變數的 SQL 命令|在變數中指定 SQL 查詢文字。|  
  
 **預覽**  
 使用 [資料檢視] 對話方塊來預覽結果。 [預覽] 最多可顯示 200 個資料列。  
  
> [!NOTE]  
>  在預覽資料時，具有 CLR 使用者定義型別的資料行不會包含資料。 而會顯示 \<數值太大而無法顯示> 或 System.Byte[]。 使用 SQL OLE DB 提供者存取資料來源時會顯示前者，而使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 提供者時會顯示後者。  
  
## 資料存取模式動態選項  
  
### 資料存取模式 = 資料表或檢視  
 **資料表或檢視的名稱**  
 從資料來源中可用的清單中選取資料表或檢視名稱。  
  
### 資料存取模式 = 資料表名稱或檢視名稱變數  
 **變數名稱**  
 請選取包含資料表或檢視名稱的變數。  
  
### 資料存取模式 = SQL 命令  
 **SQL 命令文字**  
 輸入 SQL 查詢文字，按一下 [建立查詢] 建立查詢，或按一下 [瀏覽] 找到包含查詢文字的檔案。  
  
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
 [OLE DB 來源編輯器 &#40;資料行頁面&#41;](../../integration-services/data-flow/ole-db-source-editor-columns-page.md)   
 [OLE DB 來源編輯器 &#40;錯誤輸出頁面&#41;](../../integration-services/data-flow/ole-db-source-editor-error-output-page.md)   
 [使用 OLE DB 來源來擷取資料](../../integration-services/data-flow/extract-data-by-using-the-ole-db-source.md)   
 [OLE DB 連接管理員](../../integration-services/connection-manager/ole-db-connection-manager.md)  
  
  