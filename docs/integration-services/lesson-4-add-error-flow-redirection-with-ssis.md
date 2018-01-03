---
title: "第 4 課：使用 SSIS 加入錯誤流程重新導向 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 0c8dbda2-75e3-4278-9b4e-dcd220c92522
caps.latest.revision: "24"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 60c56174d1cbfeb11f56e644eac452be2f7fcf2f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="lesson-4-add-error-flow-redirection-with-ssis"></a>第 4 課：使用 SSIS 加入錯誤流程重新導向
為了處理發生在轉換處理序中的錯誤， [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供一項功能，讓您能夠決定每一個元件和每一個資料行要如何處理無法轉換的資料。 您可以選擇忽略特定資料行的失敗、將整個失敗的資料列重新導向，或僅使該元件失敗。 依預設， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 的所有元件都設定為發生錯誤時失敗。 使元件失敗會造成封裝失敗及所有後續處理停止。  
  
若不要因為失敗而停止封裝執行，則設定及處理在轉換中可能發生的處理錯誤，是不錯的作法。 與其選擇忽略失敗以確保封裝可順利執行，不如將失敗的資料列重新導向至另一個處理路徑，讓資料和錯誤都可以保存、檢查及稍後再重新處理。  
  
在本課程中，您會建立您在 [第 3 課︰使用 SSIS 加入記錄](../integration-services/lesson-3-add-logging-with-ssis.md)所開發的套件複本。 利用這個新的封裝，您可以建立其中一個範例資料檔的損毀版本。 當您執行封裝時，損毀的檔案將強迫發生處理錯誤。  
  
為了處理錯誤資料，您會加入及設定一般檔案目的地，將在 [查閱貨幣索引鍵] 轉換中找不到查閱值的資料列寫入檔案中。  
  
將錯誤資料寫入檔案之前，您要併入一個指令碼元件，利用指令碼來取得錯誤描述。 然後您會重新設定 [查閱貨幣索引鍵] 轉換，將任何無法處理的資料重新導向至 [指令碼] 轉換。  
  
> [!IMPORTANT]  
> 這個教學課程需要 **AdventureWorksDW2012** 範例資料庫。 如需如何安裝和部署 **AdventureWorksDW2012**, [CodePlex 上的 Reporting Services 產品範例](http://go.microsoft.com/fwlink/p/?LinkID=526910)。  
  
## <a name="tasks-in-lesson"></a>本課程的工作  
這一課包含下列工作：  
  
-   [步驟 1：複製第 3 課的套件](../integration-services/lesson-4-1-copying-the-lesson-3-package.md)  
  
-   [步驟 2：建立損毀檔案](../integration-services/lesson-4-2-creating-a-corrupted-file.md)  
  
-   [步驟 3：加入錯誤流程重新導向](../integration-services/lesson-4-3-adding-error-flow-redirection.md)  
  
-   [步驟 4：加入一般檔案目的地](../integration-services/lesson-4-4-adding-a-flat-file-destination.md)  
  
-   [步驟 5：測試第 4 課的教學課程封裝](../integration-services/lesson-4-5-testing-the-lesson-4-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>開始課程  
[步驟 1：複製第 3 課的套件](../integration-services/lesson-4-1-copying-the-lesson-3-package.md)  
  
  
  
