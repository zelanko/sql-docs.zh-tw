---
title: SSIS 如何建立 ETL 套件 | Microsoft Docs
ms.custom: ''
ms.date: 04/17/2018
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- SSIS, tutorials
- packages [Integration Services], tutorials
- Integration Services, tutorials
- SQL Server Integration Services, tutorials
- logs [Integration Services], tutorials
- walkthroughs [Integration Services]
ms.assetid: d6d5bb1f-4cb1-4605-9cd6-f60b858382c4
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 83e51e583e0c83d8d0cbc8dbd213a78baa766ffb
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="ssis-how-to-create-an-etl-package"></a>SSIS 如何建立 ETL 封裝

 > 如需舊版 SQL Server 的相關內容，請參閱 [SSIS 教學課程：建立簡易 ETL 套件](https://msdn.microsoft.com/library/ms169917(SQL.120).aspx)。

在此教學課程中，您將學會如何使用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計工具來建立簡單的 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 套件。 您建立的封裝會從一般檔案取用資料，重新格式化資料，然後將重新格式化之後的資料插入到事實資料表中。 在下列課程中，將會擴充套件以示範迴圈、套件設定、記錄和錯誤流程。  
  
當您安裝了教學課程使用的範例資料時，也會安裝您在教學課程每一課中所建立套件的完整版本。 利用完整封裝，您可以三級跳，從教學課程後面的課程開始。 如果本教學課程是您初次使用套件或新開發環境，我們建議您從第 1 課開始。  

> [!IMPORTANT]
> 最近執行本教學課程所需的範例檔案無法再於先前的位置線上使用。 造成您的不便，深感抱歉。 我們已將檔案放在新的位置，並更新本文中的連結。

## <a name="what-is-sql-server-integration-services-ssis"></a>什麼是 SQL Server Integration Services (SSIS)？

[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (SSIS) 是一種用於建置高效能資料整合解決方案的平台，其中包括資料倉儲的擷取、轉換和載入 (ETL) 套件。 SSIS 包含建立和偵錯封裝的圖形工具及精靈；執行工作流程功能 (例如 FTP 作業、執行 SQL 陳述式和傳送電子郵件訊息) 的工作；擷取和載入資料的資料來源和目的地；清除、彙總、合併和複製資料的轉換；管理封裝執行和儲存的管理服務 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ；以及設計 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 物件模型之程式的應用程式開發介面 (API)。  

## <a name="what-you-learn"></a>學習內容  
要熟悉 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 所提供的新工具、控制項和功能，最好的方法就是使用它們。 這個教學課程將引導您使用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計工具來建立簡單的 ETL 套件，包括迴圈、設定、錯誤流程邏輯和記錄。  
  
## <a name="requirements"></a>需求  
這個教學課程的主要對象是熟悉基本資料庫作業，但對於 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]可用的新功能較為陌生的使用者。  
  
若要使用這個教學課程，系統上必須已安裝下列元件：  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫的 **資料庫的** 。 若要下載 **AdventureWorksDW2012** 資料庫，請從 [AdventureWorks 範例資料庫](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)下載 `AdventureWorksDW2012.bak`，並還原備份。  

-   範例資料。 範例資料隨附在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 課程封裝中。 若要將範例資料和課程套件下載為 Zip 檔案，請[按一下這裡](http://download.microsoft.com/download/3/1/4/314A4169-D540-4E9E-9776-585BFBFC2CC5/Creating a Simple ETL Package.zip)。  

## <a name="lessons-in-this-tutorial"></a>本教學課程中的課程  
[第 1 課：使用 SSIS 建立專案和基本套件](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md)  
在這一課，您會建立一個簡單的 ETL 套件。此套件會從單一的一般檔案擷取資料、使用查閱轉換來轉換資料，以及最後將結果載入事實資料表目的地。  
  
[第 2 課：使用 SSIS 加入迴圈](../integration-services/lesson-2-adding-looping-with-ssis.md)  
在這一課，您會擴充在第 1 課建立的套件，以利用新的迴圈功能，將多個一般檔案擷取到單一資料流程處理序中。  
  
[第 3 課︰使用 SSIS 加入記錄](../integration-services/lesson-3-add-logging-with-ssis.md)  
在這一課，您會擴充在第 2 課建立的套件，以利用新的記錄功能。  
  
[第 4 課：使用 SSIS 加入錯誤流程重新導向](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md)  
在這一課，您會擴充在第 3 課建立的套件，以利用新的錯誤輸出設定。  
  
[第 5 課：加入套件部署模型的 SSIS 套件組態](../integration-services/lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md)  
在這一課，您會擴充在第 4 課建立的套件，以利用新的套件設定選項。  
  
[第 6 課：在 SSIS 中搭配專案部署模型使用參數](../integration-services/lesson-6-using-parameters-with-the-project-deployment-model-in-ssis.md)  
在這一課，您會擴充在第 5 課建立的套件，以利用專案部署模型的新參數。  
  
  
  
