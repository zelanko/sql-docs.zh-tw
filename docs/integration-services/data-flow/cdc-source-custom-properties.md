---
title: "CDC 來源自訂屬性 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 744e9357-94a9-4202-abe8-1d3d202697e9
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 106f7ecb0798682b26c806ea9c2d943524dd87d4
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="cdc-source-custom-properties"></a>CDC 來源自訂屬性
  下表將描述 CDC 來源的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|說明|  
|-------------------|---------------|-----------------|  
|連接|ADO.Net 連接|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CDC 資料庫的 ADO.NET 連接，以存取變更資料表。|  
|StateVariable|字串|SSIS 字串封裝變數，用於維護目前 CDC 執行的 CDC 狀態。|  
|CdcProcessingMode|整數 (列舉)|此模式決定如何處理。 可能的選項為 [全部]、[全部 (含舊值)]、[淨]、[淨 (含更新遮罩)] 和 [淨 (含合併)]。<br /><br /> 開頭為 [全部] 的模式會傳回所有變更，開頭為 [淨] 的模式只會傳回淨變更。<br /><br /> 不含主索引鍵的資料表只可以接受 [全部] 值。<br /><br /> **Net with Update Mask**加入了名稱模式的布林資料行**__ $\<資料行名稱 >\__Changed** ，表示在目前的變更資料行變更資料列。<br /><br /> 如需此屬性之值的詳細資訊，請參閱 [CDC 來源編輯器 &#40;連線管理員頁面&#41;](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md)。|  
|CaptureInstance|字串|要讀取之 CDC 資料表的 CDC 擷取執行個體名稱。 擷取的來源資料表可以具有一個或兩個擷取執行個體，以便透過結構描述變更處理資料表定義的流暢轉換。 如果針對所擷取的來源資料表定義了多個擷取執行個體，請在此選取您想要使用的擷取執行個體。 資料表 [schema] 的預設擷取執行個體名稱。[資料表] 是\<結構描述 > _\<資料表 >，但實際擷取執行個體名稱中使用可能會不同。 從中讀取的實際資料表是 CDC 資料表**cdc。\<擷取執行個體 > _CT**。|  
|ReprocessingIndicator|布林|值，指定是否要加入 **__$reprocessing** 資料行。 此特殊輸出資料行讓 SSIS 開發人員在初始處理範圍上工作時以不同的方式處理一致性錯誤。<br /><br /> 如果為 **true**，則會加入  **__$reprocessing** 資料行。<br /><br /> 當 CDC 處理範圍與初始處理範圍 (對應至初始載入週期之 LSN 的範圍) 重疊，或者上一次執行發生錯誤之後重新處理 CDC 處理範圍時，這個資料行的值就是 **true** 。 這個指標資料行可讓 SSIS 開發人員在重新處理變更時以不同的方式處理錯誤 (例如，可以忽略刪除不存在的資料列以及在重複索引鍵上失敗的插入等動作)。<br /><br /> 預設值是 **false**秒。|  
|CommandTimeout|Integer|此值表示與 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 資料庫通訊時所用的逾時 (以秒為單位)。 當資料庫的回應時間非常慢，而且預設值 (30 秒) 不夠時，使用此值。|  
  
 如需 CDC 來源的詳細資訊，請參閱 [CDC 來源](../../integration-services/data-flow/cdc-source.md)。  
  
  

