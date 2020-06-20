---
title: CDC 來源自訂屬性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 744e9357-94a9-4202-abe8-1d3d202697e9
author: janinezhang
ms.author: janinez
ms.openlocfilehash: ebb2869899ab670a55ba2fcdafdfb1276f9207fa
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84916619"
---
# <a name="cdc-source-custom-properties"></a>CDC 來源自訂屬性
  下表將描述 CDC 來源的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|描述|  
|-------------------|---------------|-----------------|  
|Connection|ADO.Net 連接|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CDC 資料庫的 ADO.NET 連接，以存取變更資料表。|  
|StateVariable|String|SSIS 字串封裝變數，用於維護目前 CDC 執行的 CDC 狀態。|  
|CdcProcessingMode|整數 (列舉)|此模式決定如何處理。 可能的選項為 [全部]  、[全部 (含舊值)]  、[淨]  、[淨 (含更新遮罩)]  和 [淨 (含合併)]  。<br /><br /> 開頭為 [全部] 的模式會傳回所有變更，開頭為 [淨] 的模式只會傳回淨變更。<br /><br /> 不含主索引鍵的資料表只可以接受 [全部] 值。<br /><br /> **Net with Update Mask**會加入具有名稱模式 **__ $ \<column-name> \_ _Changed**的布林資料行，表示目前變更資料列中已變更的資料行。<br /><br /> 如需此屬性之值的詳細資訊，請參閱 [CDC 來源編輯器 &#40;連線管理員頁面&#41;](../cdc-source-editor-connection-manager-page.md)。|  
|CaptureInstance|String|要讀取之 CDC 資料表的 CDC 擷取執行個體名稱。 擷取的來源資料表可以具有一個或兩個擷取執行個體，以便透過結構描述變更處理資料表定義的流暢轉換。 如果針對所擷取的來源資料表定義了多個擷取執行個體，請在此選取您想要使用的擷取執行個體。 資料表 [架構] 的預設 capture 實例名稱。[table] 是 \<schema> _ \<table> ，但是使用中的實際 capture 實例名稱可能不同。 從中讀取的實際資料表是 cdc 資料表**cdc。 \<capture-instance>_CT**。|  
|ReprocessingIndicator|Boolean|值，指定是否要加入 **__$reprocessing** 資料行。 此特殊輸出資料行讓 SSIS 開發人員在初始處理範圍上工作時以不同的方式處理一致性錯誤。<br /><br /> 如果為 **true**，則會加入  **__$reprocessing** 資料行。<br /><br /> 當 CDC 處理範圍與初始處理範圍 (對應至初始載入週期之 LSN 的範圍) 重疊，或者上一次執行發生錯誤之後重新處理 CDC 處理範圍時，這個資料行的值就是 **true** 。 這個指標資料行可讓 SSIS 開發人員在重新處理變更時以不同的方式處理錯誤 (例如，可以忽略刪除不存在的資料列以及在重複索引鍵上失敗的插入等動作)。<br /><br /> 預設值為 **false**。|  
|CommandTimeout|整數|此值表示與 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 資料庫通訊時所用的逾時 (以秒為單位)。 當資料庫的回應時間非常慢，而且預設值 (30 秒) 不夠時，使用此值。|  
  
 如需 CDC 來源的詳細資訊，請參閱 [CDC 來源](cdc-source.md)。  
  
  
