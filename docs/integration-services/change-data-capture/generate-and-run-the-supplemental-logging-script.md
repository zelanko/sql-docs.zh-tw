---
title: "產生及執行補充記錄指令碼 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: change-data-capture
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- supLog
ms.assetid: 6e940d93-12c6-4cda-9333-5489b245f0e4
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ee20cd83df04d4ec3929f9ee39068969c0d18950
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="generate-and-run-the-supplemental-logging-script"></a>產生及執行補充記錄指令碼
  使用 [設定資料表來擷取變更] 頁面，於將設定補充記錄的 Oracle 來源資料庫上執行指令碼。  
  
 **若要執行補充記錄指令碼**  
  
 按一下 **[執行指令碼]** ，在針對 CDC 執行個體定義的資料表上執行補充記錄指令碼。 此指令碼會指示 Oracle 資料庫在將 UPDATE 作業記錄到擷取的資料表時，將相關的所有資料行寫入其交易記錄中。 通常是由 Oracle 系統管理員檢查和執行此指令碼。  
  
 您也可以使用 SQL * Plus 手動執行指令碼。  
  
 **若要手動執行指令碼**  
  
 按一下 **[複製]** ，將指令碼貼到剪貼簿。 開啟 SQL* Plus，然後移至包含 Oracle 來源資料庫的目錄。 將指令碼貼到 SQL\*Plus 中加以執行。  
  
 若要將補充記錄指令碼儲存在文字檔中，請按一下 **[另存新檔]** ，並瀏覽至您要儲存檔案的位置。 提供檔案名稱，然後按一下 **[儲存]** 來儲存檔案。  
  
 按 **[下一步]** ， [Generate Mirror Tables and CDC Capture Instances](../../integration-services/change-data-capture/generate-mirror-tables-and-cdc-capture-instances.md)。  
  
## <a name="see-also"></a>另請參閱  
 [如何建立 SQL Server 變更資料庫執行個體](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [檢閱及產生補充記錄指令碼](../../integration-services/change-data-capture/review-and-generate-supplemental-logging-scripts.md)  
  
  
