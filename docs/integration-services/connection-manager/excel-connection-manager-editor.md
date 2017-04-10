---
title: "Excel 連接管理員編輯器 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.excelconnection.f1"
helpviewer_keywords: 
  - "Excel 連接管理員編輯器"
ms.assetid: 7ff097e4-cafb-4885-a898-05b2a46628c1
caps.latest.revision: 32
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 32
---
# Excel 連接管理員編輯器
  使用 [Excel 連線管理員編輯器] 對話方塊，將連接加入現有或新的 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 活頁簿檔案。  
  
 若要深入了解快取連線管理員，請參閱 [Excel 連線管理員](../../integration-services/connection-manager/excel-connection-manager.md)。  
  
## 選項。  
 **Excel 檔案路徑**  
 輸入現有或新的 Excel 活頁簿檔案 (.xls) 的路徑和檔案名稱。  
  
> [!NOTE]  
>  您不能連接到受密碼保護的 Excel 檔案。  
  
> [!WARNING]  
>  當您選取指向新的或非現存檔案的 [Excel 連接]，然後在 [Excel 工作表的名稱] 中按一下 [新增] 時，[Excel 目的地編輯器] 會自動建立 Excel 檔案。  
  
 **瀏覽**  
 使用 [開啟] 對話方塊導覽至 Excel 檔存在的資料夾，或您要建立新的檔案。  
  
 **Excel 版本**  
 指定用於建立檔案的 Microsoft Excel 版本。  
  
 **第一個資料列有資料行名稱**  
 指定選取之工作表中資料的第一個資料列是否包含資料行名稱。 此選項的預設值是 **[True]**。  
  
## Microsoft Excel 和 Access 檔案的提供者和驅動程式  
 如果尚未安裝 Microsoft Office 檔案的 OLE DB 提供者及驅動程式，您必須加以下載。 新版的提供者可以開啟以舊版 Excel 建立的檔案。  
  
 如果電腦有 32 位元版本的 Office，則必須安裝 32 位元版本的驅動程式，而且您也必須確定已執行精靈或以 32 位元模式建立的 Integration Services 封裝。  
  
|Microsoft Office 版本|下載|  
|------------------------------|--------------|  
|2007|[2007 Office System 驅動程式：資料連接元件](https://www.microsoft.com/download/details.aspx?id=23734)|  
|2010|[Microsoft Access 2010 執行階段](https://www.microsoft.com/download/details.aspx?id=10910)|  
|2013|[Microsoft Access 2013 執行階段](http://www.microsoft.com/download/details.aspx?id=39358)|  
|2016|[Microsoft Access 2016 執行階段](https://www.microsoft.com/download/details.aspx?id=50040)|
  
## 請參閱＜  
 [Integration Services 錯誤和訊息參考](../../integration-services/integration-services-error-and-message-reference.md)   
 [使用 Foreach 迴圈容器來循環使用 Excel 檔案和資料表](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
  