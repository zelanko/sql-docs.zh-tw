---
title: 在 Data Quality Client 中開啟 Integration Services 專案 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: a8bad2f1-8fb0-4d14-a978-11a5720e62d6
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 9e1d315ca23b379238a19baf09ac2591d0085fad
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62792359"
---
# <a name="open-integration-services-projects-in-data-quality-client"></a>在 Data Quality Client 中開啟 Integration Services 專案
  [!INCLUDE[ssDQSCleansingLong](../includes/ssdqscleansinglong-md.md)] 可讓您以批次模式執行清理專案。 但是，有時您可能會想要在 Integration Services 封裝中檢閱清理結果，類似於在 DQS 中，於資料品質專案中清理活動內的 **[管理和檢視結果]** 索引標籤中檢閱清理結果。 DQS 可讓您在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 中開啟 Integration Services 專案，就像從 **[開啟專案]** 畫面開啟其他任何資料品質專案，並讓您擁有在 Integration Services 專案中清理結果的互動式清理體驗。  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="LimitationsRestrictions"></a> 限制事項  
  
-   **中的** [開啟專案] [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]畫面上只會提供完成的 Integration Services 專案。 **[開啟專案]** 畫面上不會提供失敗或執行中的專案。  
  
-   Integration Services 專案會在**中的互動式清理階段開啟 (** [管理和檢視結果] [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]索引標籤)。 您不能移至 **[清理]** 或 **[對應]** 索引標籤。 您只能按 **[下一步]** 移至 **[匯出]** 索引標籤。  
  
-   您無法從 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]刪除鎖定的 Integration Services 專案。 您必須先解除鎖定，然後才能刪除。  
  
###  <a name="Prerequisites"></a> 必要條件  
 您必須已經順利執行完 Integration Services 專案 (其中包含的封裝具有 DQS 清理元件)，才能在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]中加以查看及開啟。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 您必須擁有 DQS_MAIN 資料庫的 dqs_kb_editor 或 dqs_kb_operator 角色，才能開啟 Integration Services 專案。  
  
##  <a name="Open"></a> 開啟 Integration Services 專案  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [執行 Data Quality Client 應用程式](../../2014/data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面中，按一下 **[開啟資料品質專案]**。 **[開啟專案]** 畫面隨即出現。  
  
3.  在 **[開啟專案]** 畫面上，您可以依照以下其中一種方式來識別 Integration Services 專案：  
  
    1.  **專案名稱**：Integration Services 專案會使用下列命名術語列出：「 Package.DQS Cleansing_*\<日期 > * *\<時間 >*_ {GUID}。 」 每次在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中成功執行相同的封裝時，新的專案會列在 [開啟專案]  畫面中。  
  
    2.  **專案類型**：Integration Services 專案在 [開啟專案] 畫面上擁有 [SSIS] 專案類型。  
  
     選取專案，然後按 **[下一步]**。  
  
4.  Integration Services 專案會在互動式清理階段開啟 (**[管理和檢視結果]** 索引標籤)。 您可以針對 Integration Services 專案中的資料執行互動式清理。 如需 [管理和檢視結果] 索引標籤的詳細資訊，請參閱[使用 DQS &#40;內部&#41; 知識清理資料](../../2014/data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)中的[互動式清理階段](../../2014/data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Interactive)。  
  
5.  按 **[下一步]** 移至 **[匯出]** 索引標籤，您可以在這裡將處理過的資料匯出到以下任何項目：SQL Server 資料庫中的新資料表、.csv 檔案或 Excel 檔案。 如需 [匯出] 索引標籤的詳細資訊，請參閱[使用 DQS &#40;內部&#41; 知識清理資料](../../2014/data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)中的[匯出階段](../../2014/data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Export)。  
  
6.  在匯出資料之後，按一下 **[完成]** ，關閉 Integration Services 專案。  
  
## <a name="see-also"></a>另請參閱  
 [DQS 清理轉換](../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)   
 [Integration Services &#40;SSIS&#41; 專案](../integration-services/integration-services-ssis-projects-and-solutions.md)  
