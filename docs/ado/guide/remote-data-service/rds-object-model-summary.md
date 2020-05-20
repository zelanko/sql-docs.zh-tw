---
title: RDS 物件模型摘要 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS objects [ADO], object model summary
- RDS object model [ADO]
ms.assetid: 909f9af7-31db-4eec-ad52-650ce74dac2f
author: rothja
ms.author: jroth
ms.openlocfilehash: 95ddd84bfd755e044d97a6043f295014933ae18c
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763589"
---
# <a name="rds-object-model-summary"></a>RDS 物件模型摘要
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
|Object|描述|  
|------------|-----------------|  
|[RDS.DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)|這個物件包含取得伺服器 proxy 的方法。 Proxy 可以是預設或自訂伺服器程式（商務物件）。 伺服器程式可在網際網路、內部網路、區域網路或本機動態程式庫上叫用。<br /><br /> 「**空間**」物件可安全地進行腳本處理。|  
|[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|此物件代表預設的伺服器程式。 它會執行預設的 RDS 資料抓取和更新行為。<br /><br /> 撰寫腳本時， **DataFactory**物件是不安全的。|  
|[RDS.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)|這個物件可以自動叫用**RDS。[空間**] 和 [ **RDSServer] DataFactory**物件。<br /><br /> 使用此物件來叫用預設的 RDS 資料抓取或更新行為。<br /><br /> 這個物件也會提供視覺控制項用來存取傳回之**記錄集**物件的方法。<br /><br /> **DataControl**物件可安全地進行腳本處理。|  
  
## <a name="see-also"></a>另請參閱  
 [RDS 基本概念](../../../ado/guide/remote-data-service/rds-fundamentals.md)   
 [RDS 案例](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 教學課程](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [RDS 提供使用方式與安全性](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


