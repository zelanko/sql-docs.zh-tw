---
title: 具有物件的 RDS 程式設計模型 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 5f41fd577b470493aa6a53c8ea9ad760287a3507
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82747749"
---
# <a name="rds-programming-model-with-objects"></a>具有物件的 RDS 程式設計模型
RDS 的目標是要透過像是 IIS 的媒介來取得及更新資料來源。 程式設計模型會指定完成此目標所需的活動順序。 物件模型會指定其方法和屬性會影響程式設計模型的物件。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 RDS 提供執行下列動作順序的方法：  
  
-   指定要在伺服器上叫用的程式，並從用戶端（RDS）取得方法（proxy）來參考它[。空間](../../../ado/reference/rds-api/dataspace-object-rds.md)）。  
  
-   叫用伺服器程式。 將參數傳遞給識別資料來源的伺服器程式，以及要發出的命令（proxy 或[RDS）。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)）。  
  
-   伺服器程式會從資料來源取得[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件，通常是使用 ADO。 （選擇性）在伺服器上處理**記錄集**物件（[RDSServer. DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)）。  
  
-   伺服器程式會將最終的**記錄集**物件傳回至用戶端應用程式（proxy）。  
  
-   在用戶端上，**記錄集**物件會放入一個表單中，視覺控制項（visual Control 和 RDS）可以輕鬆地使用它 **。DataControl**）。  
  
-   對**記錄集**物件所做的變更會傳送回伺服器，並用來更新資料來源（**RDS）。DataControl**或**RDSServer. DataFactory**）。  
  
## <a name="see-also"></a>另請參閱  
 [RDS 物件模型摘要](../../../ado/guide/remote-data-service/rds-object-model-summary.md)   
 [DataControl 物件（RDS）](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [DataFactory 物件（RDSServer）](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [空間物件（RDS）](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [RDS 案例](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 教學課程](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Recordset 物件（ADO）](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [RDS 提供使用方式與安全性](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


