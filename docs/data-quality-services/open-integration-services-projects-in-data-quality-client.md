---
title: "在 Data Quality Client 中開啟 Integration Services 專案 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a8bad2f1-8fb0-4d14-a978-11a5720e62d6
caps.latest.revision: "9"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8f4785aad9a7edc6681355655a70acec194231c4
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="open-integration-services-projects-in-data-quality-client"></a>在 Data Quality Client 中開啟 Integration Services 專案
  Integration Services 的 DQS 清理元件可讓您以批次模式執行清理專案。 但是，有時您可能會想要在 Integration Services 封裝中檢閱清理結果，類似於在 DQS 中，於資料品質專案中清理活動內的 **[管理和檢視結果]** 索引標籤中檢閱清理結果。 DQS 可讓您在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 中開啟 Integration Services 專案，就像從 **[開啟專案]** 畫面開啟其他任何資料品質專案，並讓您擁有在 Integration Services 專案中清理結果的互動式清理體驗。  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="LimitationsRestrictions"></a> 限制事項  
  
-   **中的** [開啟專案] [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]畫面上只會提供完成的 Integration Services 專案。 **[開啟專案]** 畫面上不會提供失敗或執行中的專案。  
  
-   Integration Services 專案會在**中的互動式清理階段開啟 (** [管理和檢視結果] [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]索引標籤)。 您不能移至 **[清理]** 或 **[對應]** 索引標籤。 您只能按 **[下一步]** 移至 **[匯出]**索引標籤。  
  
-   您無法從 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]刪除鎖定的 Integration Services 專案。 您必須先解除鎖定，然後才能刪除。  
  
###  <a name="Prerequisites"></a> 必要條件  
 您必須已經順利執行完 Integration Services 專案 (其中包含的封裝具有 DQS 清理元件)，才能在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]中加以查看及開啟。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 您必須擁有 DQS_MAIN 資料庫的 dqs_kb_editor 或 dqs_kb_operator 角色，才能開啟 Integration Services 專案。  
  
  
##  <a name="Open"></a> 開啟 Integration Services 專案  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [執行 Data Quality Client 應用程式](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面中，按一下 **[開啟資料品質專案]**。 **[開啟專案]** 畫面隨即出現。  
  
3.  在 **[開啟專案]** 畫面上，您可以依照以下其中一種方式來識別 Integration Services 專案：  
  
    1.  **專案名稱**：Integration Services 專案會使用以下命名術語列出：“Package.DQS Cleansing_*\<DATE>**\<TIME>*_{GUID}”。 每次在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中成功執行相同的封裝時，新的專案會列在 [開啟專案]  畫面中。  
  
    2.  **專案類型**：Integration Services 專案在 **[開啟專案]** 畫面上擁有 **[SSIS]** 專案類型。  
  
     選取專案，然後按 **[下一步]**。  
  
4.  Integration Services 專案會在互動式清理階段開啟 (**[管理和檢視結果]** 索引標籤)。 您可以針對 Integration Services 專案中的資料執行互動式清理。 如需 [管理和檢視結果] 索引標籤的詳細資訊，請參閱[使用 DQS &#40;內部&#41; 知識清理資料](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)中的[互動式清理階段](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Interactive)。  
  
5.  按 **[下一步]** 移至 **[匯出]** 索引標籤，您可以在這裡將處理過的資料匯出到以下任何項目：SQL Server 資料庫中的新資料表、.csv 檔案或 Excel 檔案。 如需 [匯出] 索引標籤的詳細資訊，請參閱[使用 DQS &#40;內部&#41; 知識清理資料](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)中的[匯出階段](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Export)。  
  
6.  在匯出資料之後，按一下 **[完成]** ，關閉 Integration Services 專案。  

  
## <a name="see-also"></a>另請參閱  
 [DQS 清理轉換](../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)   
 [Integration Services (SSIS) 專案](../integration-services/integration-services-ssis-projects-and-solutions.md)  
  
  
