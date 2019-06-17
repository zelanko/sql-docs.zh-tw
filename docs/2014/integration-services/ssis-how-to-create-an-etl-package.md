---
title: SSIS 教學課程：建立簡易 ETL 套件 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS, tutorials
- packages [Integration Services], tutorials
- Integration Services, tutorials
- SQL Server Integration Services, tutorials
- logs [Integration Services], tutorials
- walkthroughs [Integration Services]
ms.assetid: d6d5bb1f-4cb1-4605-9cd6-f60b858382c4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e25c90b3baa4e718f40dc3a3f84b6dc221d54c33
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62878280"
---
# <a name="ssis-tutorial-creating-a-simple-etl-package"></a>SSIS 教學課程：建立簡易 ETL 封裝
  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (SSIS) 是用於建立高效能資料整合方案，包括擷取、 轉換和載入 (ETL) 封裝的資料倉儲的平台。 SSIS 包含建立和偵錯封裝的圖形工具及精靈；執行工作流程功能 (例如 FTP 作業、執行 SQL 陳述式和傳送電子郵件訊息) 的工作；擷取和載入資料的資料來源和目的地；清除、彙總、合併和複製資料的轉換；管理封裝執行和儲存的管理服務 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ；以及設計 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 物件模型之程式的應用程式開發介面 (API)。  
  
 在此教學課程中，您將學會如何使用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師來建立簡單的 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝。 您建立的封裝會從一般檔案取用資料，重新格式化資料，然後將重新格式化之後的資料插入到事實資料表中。 在下列課程中，將會擴充封裝來示範迴圈、封裝組態、記錄和錯誤流程。  
  
 當您安裝教學課程使用的範例資料時，也會安裝您將在教學課程每一課所建立之封裝的完整版本。 利用完整封裝，您可以三級跳，從教學課程後面的課程開始。 如果這是您第一次使用封裝或新的開發環境，我們建議您從第 1 課開始。  
  
## <a name="what-you-will-learn"></a>學習內容  
 要熟悉 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 所提供的新工具、控制項和功能，最好的方法就是使用它們。 這個教學課程引導您使用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師來建立簡單的 ETL 封裝，包括迴圈、組態、錯誤流程邏輯和記錄。  
  
## <a name="requirements"></a>需求  
 這個教學課程的主要對象是熟悉基本資料庫作業，但對於 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]可用的新功能較為陌生的使用者。  
  
 若要使用這個教學課程，系統上必須已安裝下列元件：  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫的 **資料庫的** 。 為了加強安全性，依預設，不會安裝範例資料庫。 若要下載 **AdventureWorksDW2012** 資料庫，請參閱 [Adventure Works for SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=275026)。  
  
    > [!IMPORTANT]  
    >  當您附加資料庫 (\*.mdf 檔案) 時， [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 預設會搜尋 .ldf 檔案。 您必須先手動移除 .ldf 檔案，然後再按一下 **[附加資料庫]** 對話方塊中的 [確定]。  
    >   
    >  如需有關附加資料庫的詳細資訊，請參閱＜ [Attach a Database](../relational-databases/databases/attach-a-database.md)＞。  
  
-   範例資料。 範例資料隨附在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 課程封裝中。 若要下載範例資料和課程封裝，請執行下列動作。  
  
    1.  導覽至 [Integration Services 產品範例](https://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  按一下 **[下載]** 索引標籤。  
  
    3.  按一下 SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip 檔案。  
  
## <a name="lessons-in-this-tutorial"></a>本教學課程中的課程  
 [第 1 課：建立專案和基本套件](lesson-1-create-a-project-and-basic-package-with-ssis.md)  
 在這一課，您將建立一個從單個一般檔案擷取資料的簡易 ETL 封裝，使用查閱轉換元件來轉換資料，最後將結果載入至事實資料表目的地。  
  
 [第 2 課：加入迴圈](lesson-2-adding-looping-with-ssis.md)  
 在這一課，您將擴充在第 1 課建立的封裝，利用新的迴圈功能，將多個一般檔案擷取到單一資料流程處理序中。  
  
 [第 3 課：新增記錄](lesson-3-add-logging-with-ssis.md)  
 在這一課，您將擴充在第 2 課建立的封裝，來利用新的記錄功能。  
  
 [第 4 課：加入錯誤流程重新導向](lesson-4-add-error-flow-redirection-with-ssis.md)  
 在這一課，您將擴充在第 3 課建立的封裝，來利用新的錯誤輸出組態。  
  
 [第 5 課：加入封裝部署模型的封裝組態](lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md)  
 在這一課，您將擴充在第 4 課建立的封裝，來利用新的封裝組態選項。  
  
 [第 6 課：搭配專案部署模型使用參數](lesson-6-using-parameters-with-the-project-deployment-model-in-ssis.md)  
 在這一課，您將擴充在第 5 課建立的封裝，以充分搭配專案部署模型來使用新的參數。  
  
  
