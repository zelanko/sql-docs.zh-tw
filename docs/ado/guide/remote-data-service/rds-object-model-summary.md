---
description: RDS 物件模型摘要
title: RDS 物件模型摘要 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: e2650f9a80c56856133d1e694a5ea0eb807251f0
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88977979"
---
# <a name="rds-object-model-summary"></a>RDS 物件模型摘要
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
|Object|描述|  
|------------|-----------------|  
|[RDS.DataSpace](../../reference/rds-api/dataspace-object-rds.md)|此物件包含取得伺服器 proxy 的方法。 Proxy 可能是預設或自訂伺服器程式 (商務物件) 。 您可以在網際網路、內部網路、區域網路或本機動態程式庫上叫用伺服器程式。<br /><br /> 您可以安全地執行腳本處理的 **空間** 物件。|  
|[RDSServer.DataFactory](../../reference/rds-api/datafactory-object-rdsserver.md)|此物件代表預設的伺服器程式。 它會執行預設的 RDS 資料抓取和更新行為。<br /><br /> **DataFactory**物件對腳本而言並不安全。|  
|[RDS.DataControl](../../reference/rds-api/datacontrol-object-rds.md)|此物件可以自動叫用 **RDS。空間** 和 **RDSServer. DataFactory** 物件。<br /><br /> 使用這個物件來叫用預設的 RDS 資料抓取或更新行為。<br /><br /> 這個物件也提供視覺控制項存取傳回的 **記錄集** 物件的方法。<br /><br /> **DataControl**物件對腳本是安全的。|  
  
## <a name="see-also"></a>另請參閱  
 [RDS 基本概念](./rds-fundamentals.md)   
 [RDS 案例](./rds-scenario.md)   
 [RDS 教學課程](./rds-tutorial.md)   
 [RDS 使用方式與安全性](./rds-usage-and-security.md)