---
title: 產生及執行補充記錄指令碼 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- supLog
ms.assetid: 6e940d93-12c6-4cda-9333-5489b245f0e4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b5bfbff70d29e2b7b18c82b323d3ab34a3c6c60e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62835473"
---
# <a name="generate-and-run-the-supplemental-logging-script"></a>產生及執行補充記錄指令碼
  使用 [設定資料表來擷取變更] 頁面，於將設定補充記錄的 Oracle 來源資料庫上執行指令碼。  
  
 **若要執行補充記錄指令碼**  
  
 按一下 **[執行指令碼]** ，在針對 CDC 執行個體定義的資料表上執行補充記錄指令碼。 此指令碼會指示 Oracle 資料庫在將 UPDATE 作業記錄到擷取的資料表時，將相關的所有資料行寫入其交易記錄中。 通常是由 Oracle 系統管理員檢查和執行此指令碼。  
  
 您也可以使用 SQL * Plus 手動執行指令碼。  
  
 **若要手動執行指令碼**  
  
 按一下 **[複製]** ，將指令碼貼到剪貼簿。 開啟 SQL* Plus，然後移至包含 Oracle 來源資料庫的目錄。 將指令碼貼到 SQL\*Plus 中加以執行。  
  
 若要將補充記錄指令碼儲存在文字檔中，請按一下 **[另存新檔]** ，並瀏覽至您要儲存檔案的位置。 提供檔案名稱，然後按一下 **[儲存]** 來儲存檔案。  
  
 按 **[下一步]** ， [Generate Mirror Tables and CDC Capture Instances](generate-mirror-tables-and-cdc-capture-instances.md)。  
  
## <a name="see-also"></a>另請參閱  
 [如何建立 SQL Server 變更資料庫執行個體](how-to-create-the-sql-server-change-database-instance.md)   
 [檢閱及產生補充記錄指令碼](review-and-generate-supplemental-logging-scripts.md)  
  
  
