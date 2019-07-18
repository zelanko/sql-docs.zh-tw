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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6c455d816b3ba5a9606d09e3b05e54583e11ca41
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922536"
---
# <a name="rds-object-model-summary"></a>RDS 物件模型摘要
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
|Object|描述|  
|------------|-----------------|  
|[RDS.DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)|此物件包含方法，以取得伺服器的 proxy。 預設或自訂伺服器程式 （商務物件），可能是 proxy。 伺服器程式可能會在網際網路、 近端內部網路、 區域網路上，叫用，或者是本機的動態連結程式庫。<br /><br /> **DataSpace**物件而言是安全的指令碼。|  
|[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|這個物件所表示的預設伺服器程式。 它會執行預設 RDS 資料擷取和更新行為。<br /><br /> **DataFactory**物件不是安全的。|  
|[RDS.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)|這個物件可以自動叫用**rds。DataSpace**並**RDSServer.DataFactory**物件。<br /><br /> 您可以使用此物件來叫用預設 RDS 資料擷取或更新行為。<br /><br /> 這個物件也會提供方法來存取傳回的視覺控制項**資料錄集**物件。<br /><br /> **DataControl**物件而言是安全的指令碼。|  
  
## <a name="see-also"></a>另請參閱  
 [RDS 基本概念](../../../ado/guide/remote-data-service/rds-fundamentals.md)   
 [RDS 案例](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 教學課程](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [RDS 提供使用方式與安全性](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


