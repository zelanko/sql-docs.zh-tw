---
title: "檢閱及產生補充記錄指令碼 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: change-data-capture
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: scripts
ms.assetid: 5c858ae2-37d6-42e8-a252-7f6ed4e628a7
caps.latest.revision: "6"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7b5587d6def935cf31d4bf96056b21cfd2c263a1
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="review-and-generate-supplemental-logging-scripts"></a>檢閱及產生補充記錄指令碼
  使用 [指令碼] 索引標籤可在設定補充記錄的 Oracle 來源資料庫上執行或重新執行指令碼。  
  
 在您執行指令碼之前，請選取下列其中一項：  
  
 **在此工作階段中包含變更**  
 選取這個選項，在已加入至 CDC 執行個體的任何新資料表上或是透過屬性編輯器以任何方式變更的資料表上執行指令碼。  
  
> [!NOTE]  
>  如果未針對 CDC 執行個體中的資料表進行任何變更，則 Oracle 補充記錄指令碼區域會是空的。  
  
 **包含所有資料表/擷取執行個體**  
 選取這個選項，在 CDC 執行個體的所有資料表和擷取執行個體上執行指令碼。  
  
 當您選取其中一個選項之後，請執行補充記錄指令碼。  
  
### <a name="to-run-the-supplemental-logging-scripts"></a>若要執行補充記錄指令碼  
  
1.  按一下 **[執行指令碼]** ，在針對 CDC 執行個體定義的資料表上執行補充記錄指令碼。 此指令碼會指示 Oracle 資料庫在將 UPDATE 作業記錄到擷取的資料表時，將相關的所有資料行寫入其交易記錄中。 通常是由 Oracle 系統管理員檢查和執行此指令碼。  
  
2.  當您執行補充記錄指令碼時，將會開啟 [執行指令碼的 Oracle 認證] 對話方塊，您可以在此提供有效的 Oracle 使用者名稱和密碼。 如需有關如何提供適當之 Oracle 認證的詳細資訊，請參閱＜ [Oracle Credentials for Running Script](../../integration-services/change-data-capture/oracle-credentials-for-running-script.md)＞。  
  
 必要時，您也可以使用 SQL * Plus 手動執行指令碼。  
  
### <a name="to-run-the-scripts-manually"></a>若要手動執行指令碼  
  
1.  按一下 **[複製]** ，將指令碼貼到剪貼簿。 開啟 SQL* Plus，然後移至包含 Oracle 來源資料庫的目錄。 將指令碼貼到 SQL\*Plus 中加以執行。  
  
### <a name="to-save-the-supplemental-logging-script-in-a-text-file"></a>若要將補充記錄指令碼儲存到文字檔中  
  
1.  按一下 **[另存新檔]** ，並瀏覽至您想要儲存檔案的位置。  
  
2.  提供檔案名稱，然後按一下 **[儲存]** 來儲存檔案。  
  
## <a name="see-also"></a>另請參閱  
 [如何編輯 CDC 執行個體屬性](../../integration-services/change-data-capture/how-to-edit-the-cdc-instance-properties.md)   
 [執行指令碼的 Oracle 認證](../../integration-services/change-data-capture/oracle-credentials-for-running-script.md)  
  
  
