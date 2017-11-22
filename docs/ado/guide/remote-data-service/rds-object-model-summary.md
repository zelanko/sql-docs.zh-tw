---
title: "RDS 物件模型摘要 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RDS objects [ADO], object model summary
- RDS object model [ADO]
ms.assetid: 909f9af7-31db-4eec-ad52-650ce74dac2f
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b68f17999d9b6c74155463525ca04d6c000cd23f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="rds-object-model-summary"></a>RDS 物件模型摘要
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
|物件|Description|  
|------------|-----------------|  
|[RDS資料空間](../../../ado/reference/rds-api/dataspace-object-rds.md)|此物件包含方法，以取得伺服器 proxy。 Proxy 可能是預設或自訂伺服器的程式 （商務物件）。 伺服器程式可在網際網路、 內部網路、 區域網路上，叫用，或者是本機的動態連結程式庫。<br /><br /> **DataSpace**物件而言是安全的指令碼。|  
|[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|這個物件代表的預設伺服器程式。 它會執行預設 RDS 資料擷取和更新行為。<br /><br /> **DataFactory**物件不是安全的。|  
|[RDSDataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)|這個物件可以自動叫用**.RDSDataSpace**和**RDSServer.DataFactory**物件。<br /><br /> 使用此物件來叫用預設 RDS 資料擷取或更新的行為。<br /><br /> 這個物件也會提供的方式來存取傳回的視覺控制項**資料錄集**物件。<br /><br /> **DataControl**物件而言是安全的指令碼。|  
  
## <a name="see-also"></a>請參閱＜  
 [RDS 的基本概念](../../../ado/guide/remote-data-service/rds-fundamentals.md)   
 [RDS 案例](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 教學課程](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [RDS 提供使用方式與安全性](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


