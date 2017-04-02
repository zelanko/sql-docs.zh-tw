---
title: "在 Data Quality Client 中開啟 Integration Services 專案 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a8bad2f1-8fb0-4d14-a978-11a5720e62d6
caps.latest.revision: 9
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 9
---
# 在 Data Quality Client 中開啟 Integration Services 專案
  Integration Services 的 DQs 清理元件可讓您在批次模式中執行清理專案。 不過，有時候您可能想要檢閱清理結果類似於如何檢閱清理結果中的 Integration Services 封裝中 **管理和檢視結果** 清理活動在 DQS 中的資料品質專案] 索引標籤。 DQS 可讓您開啟中的 Integration Services 專案 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 就像任何其他資料品質專案 **開啟專案** 畫面上，與在 Integration Services 專案中清理結果的互動式清理體驗。  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="LimitationsRestrictions"></a> 限制事項  
  
-   完成專案所提供的整合服務僅 **開啟專案** 畫面 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]。 失敗或執行專案中沒有 **開啟專案** 畫面。  
  
-   在互動式清理階段中開啟 integration Services 專案 (**管理和檢視結果** ] 索引標籤) 中 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]。 您不能移至 **清理** 或 **對應** 索引標籤。 您只可以移至 **匯出** ] 索引標籤，即可 **下一步**。  
  
-   您無法從 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 刪除鎖定的 Integration Services 專案。 您必須先解除鎖定，然後才能刪除。  
  
###  <a name="Prerequisites"></a> 必要條件  
 您必須已經順利執行完 Integration Services 專案包含的封裝中加以查看及開啟 DQS 清理元件 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 您必須擁有 DQS_MAIN 資料庫的 dqs_kb_editor 或 dqs_kb_operator 角色，才能開啟 Integration Services 專案。  
  
  
##  <a name="Open"></a> 開啟 Integration Services 專案  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [執行資料品質用戶端應用程式](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面中，按一下 [ **開啟資料品質專案**。 **[開啟專案]** 畫面隨即出現。  
  
3.  在 **開啟專案** ] 畫面中，您可以識別 Integration Services 專案中以下列方式之一︰  
  
    1.  **專案名稱**: Integration Services 專案會使用以下命名術語列出: 「 Package.DQS Cleansing_*\< 日期>**\< 時間>*_ {GUID}。 」 每次成功執行相同的封裝 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], ，新的專案是否列在 **開啟專案** 畫面。  
  
    2.  **專案類型**: Integration Services 專案具有 **SSIS** 做為專案類型中 **開啟專案** 畫面。  
  
     選取專案，然後按一下 [ **下一步**。  
  
4.  Integration Services 專案會在互動式清理階段開啟 (**管理和檢視結果** ] 索引標籤)。 您可以針對 Integration Services 專案中的資料執行互動式清理。 如需詳細資訊 **管理和檢視結果** 索引標籤上，請參閱 [互動式清理階段](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Interactive) 中 [使用 DQS 清理資料 #40，供內部使用 &#41;知識](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)。  
  
5.  按一下 [ **下一步** 前往 **匯出** ] 索引標籤，您可以將處理過的資料匯出至下列任一項︰ SQL Server 資料庫、.csv 檔案或 Excel 檔案中的新資料表。 如需詳細資訊 **匯出** 索引標籤上，請參閱 [匯出階段](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Export) 中 [使用 DQS 清理資料 #40，供內部使用 &#41;知識](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)  
  
6.  匯出資料之後, 按一下 **完成** ，關閉 Integration Services 專案。  

  
## 另請參閱  
 [DQS 清理轉換](../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)   
 [Integration Services (SSIS) 專案](https://msdn.microsoft.com/library/ms138028.aspx)  
  
  