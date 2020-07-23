---
title: CDC 控制工作自訂屬性 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 2a073699-79a2-4ea1-a68e-fc17a80b74ba
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ce75fa54fab43d7f84defd065ffd88111ffda542
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86923726"
---
# <a name="cdc-control-task-custom-properties"></a>CDC 控制工作自訂屬性

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  下表描述 CDC 控制工作的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|描述|  
|-------------------|---------------|-----------------|  
|Connection|ADO.NET 連接|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CDC 資料庫的 ADO.NET 連接，以存取變更資料表和 CDC 狀態 (如果儲存在相同的資料庫中)。<br /><br /> 此連接必須指向啟用 CDC 而且包含選取之變更資料表的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。|  
|TaskOperation|整數 (列舉)|CDC 控制工作的選定作業。 可能值為 **[標記初始載入開始]** 、 **[標記初始載入結束]** 、 **[標記 CDC 開始]** 、 **[取得處理範圍]** 、 **[標記處理的範圍]** 和 **[重設 CDC 狀態]** 。<br /><br /> 如果您在 **CDC (亦即，非 Oracle) 上工作時選取了**MarkCdcStart **、** MarkInitialLoadStart **或** MarkInitialLoadEnd [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，連線管理員中指定的使用者就必須是  **db_owner** 或 **系統管理員**。<br /><br /> 如需有關這些作業的詳細資訊，請參閱＜ [CDC Control Task Editor](../../integration-services/control-flow/cdc-control-task-editor.md) ＞和＜ [CDC Control Task](../../integration-services/control-flow/cdc-control-task.md)＞。|  
|OperationParameter|String|目前用於 **MarkCdcStart** 作業。 此參數允許特定作業所需的額外輸入。 例如， **MarkCdcStart** 作業所需的 LSN 號碼。|  
|StateVariable|String|SSIS 封裝變數，儲存目前 CDC 內容的 CDC 狀態。 CDC 控制工作會將狀態讀寫至 **StateVariable** ，而且不會在永續性儲存體中載入或儲存它，除非已選取 **AutomaticStatePersistence** 。 請參閱 [定義狀態變數](../../integration-services/data-flow/define-a-state-variable.md)。|  
|AutomaticStatePersistence|Boolean|CDC 控制工作會從 CDC 狀態封裝變數中讀取 CDC 狀態。 在作業之後，CDC 控制工作會更新 CDC 狀態封裝變數的值。 **AutomaticStatePersistence** 屬性告知 CDC 控制工作，誰負責在 SSIS 封裝執行之間保存 CDC 狀態值。<br /><br /> 如果此屬性為 **true**，CDC 控制工作會自動從狀態資料表中載入 CDC 狀態變數的值。 當 CDC 控制工作更新 CDC 狀態變數的值時，它也會更新相同狀態 **資料表中的其值，將狀態儲存**在特殊資料表中，以及更新狀態變數。 開發人員可以控制哪個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫包含該狀態資料表及其名稱。 此狀態資料表的結構是預先定義的。<br /><br /> 如果為 **false**，CDC 控制工作就不會處理其值的保存。 如果為 true，CDC 控制工作會將狀態儲存在特殊資料表中，並更新 StateVariable。<br /><br /> 預設值是 **true**，表示狀態持續性會自動更新。|  
|StateConnection|ADO.NET 連接|ADO.NET 連接，指向使用 **AutomaticStatePersistence**時狀態資料表所在的資料庫。 預設值是 **Connection**的相同值。|  
|StateName|String|與永續性狀態相關聯的名稱。 使用相同 CDC 內容的完整載入和 CDC 封裝都會指定通用 CDC 內容名稱。 這個名稱是用於查閱狀態資料表中的狀態資料列。<br /><br /> 此屬性只在 **AutomaticStatePersistence** 設為 **true**時才適用。|  
|StateTable|String|指定 CDC 內容狀態儲存所在的資料表名稱。 此資料表必須可透過為此元件設定的連接進行存取。 此資料表必須包含名為 **name** 和 **state**的 varchar 資料行 ( **state** 資料行必須至少有 256 個字元)。<br /><br /> 此屬性只在 **AutomaticStatePersistence** 設為 **true**時才適用。|  
|CommandTimeout|integer|此值表示與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫通訊時所用的逾時 (以秒為單位)。 當資料庫的回應時間非常慢，而且預設值 (30 秒) 不夠時，使用此值。|  
  
## <a name="see-also"></a>另請參閱  
 [CDC Control Task](../../integration-services/control-flow/cdc-control-task.md)   
 [CDC 控制工作編輯器](../../integration-services/control-flow/cdc-control-task-editor.md)  
  
  
