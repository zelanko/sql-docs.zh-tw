---
title: "RDS 程式設計模型與物件 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RDS programming model [ADO]
- RDS objects [ADO]
ms.assetid: 07ce0ef0-72f1-48f4-823d-1b65d28c0926
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2f89c867cb836ec69fd5fe59adf16d93f4708d0f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="rds-programming-model-with-objects"></a>RDS 與物件的程式設計模型
RDS 的目標為存取和更新的媒介，例如 IIS 透過資料來源。 程式設計模型指定的活動所需達成此目標的序列。 物件模型中指定的物件，其方法和屬性會影響的程式設計模型。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 RDS 提供方法來執行下列動作順序：  
  
-   指定要在伺服器上，叫用的程式，並取得 (proxy) 參考方法，從用戶端 ([.RDSDataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md))。  
  
-   叫用伺服器程式。 將參數傳遞至伺服器程式的識別資料來源以及要發出的命令 (proxy 或[.RDSDataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md))。  
  
-   伺服器程式會取得[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)來自資料來源，通常是透過使用 ADO 的物件。 （選擇性）**資料錄集**在伺服器上處理物件 ([RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md))。  
  
-   伺服器程式傳回最終**資料錄集**用戶端應用程式 (proxy) 的物件。  
  
-   在用戶端，**資料錄集**物件放入一個表單，可能容易使用的視覺控制項 (visual 控制項和**.RDSDataControl**)。  
  
-   若要變更**資料錄集**物件傳送至伺服器及用來更新資料來源 (**.RDSDataControl**或**RDSServer.DataFactory**)。  
  
## <a name="see-also"></a>另請參閱  
 [RDS 物件模型摘要](../../../ado/guide/remote-data-service/rds-object-model-summary.md)   
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [DataFactory 物件 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [資料空間物件 (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [RDS 案例](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 教學課程](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [RDS 提供使用方式與安全性](../../../ado/guide/remote-data-service/rds-usage-and-security.md)



