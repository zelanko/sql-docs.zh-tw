---
title: RDS 程式設計模型與物件 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS programming model [ADO]
- RDS objects [ADO]
ms.assetid: 07ce0ef0-72f1-48f4-823d-1b65d28c0926
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b60f402cdc7ba861a0d0550a92d16fa7dd1f59b7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62931420"
---
# <a name="rds-programming-model-with-objects"></a>具有物件的 RDS 程式設計模型
RDS 的目標是取得存取權，以及更新資料來源，透過例如 IIS 媒介。 程式設計模型指定完成這個目標所需的活動的序列。 物件模型會指定其方法和屬性會影響程式設計模型的物件。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 RDS 提供方法來執行下列動作順序：  
  
-   指定要在伺服器上，叫用的程式，並取得用戶端從參考它的方式 (proxy) ([rds。DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md))。  
  
-   叫用伺服器程式。 將參數傳遞至伺服器程式識別資料來源以及要發出的命令 (proxy 或[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md))。  
  
-   伺服器程式會取得[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)從資料來源，通常是藉由使用 ADO 的物件。 （選擇性） **Recordset**伺服器上處理物件 ([RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md))。  
  
-   伺服器程式會傳回最後**資料錄集**用戶端應用程式 (proxy) 的物件。  
  
-   在用戶端**資料錄集**物件會放入容易使用的視覺控制項的表單 (視覺控制項和**rds。DataControl**)。  
  
-   若要變更**Recordset**物件傳送至伺服器及用來更新資料來源 (**RDSDataControl**或是**RDSServer.DataFactory**)。  
  
## <a name="see-also"></a>另請參閱  
 [RDS 物件模型摘要](../../../ado/guide/remote-data-service/rds-object-model-summary.md)   
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [DataFactory 物件 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [DataSpace Object (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [RDS 案例](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 教學課程](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [RDS 提供使用方式與安全性](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


