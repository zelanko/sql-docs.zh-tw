---
description: 具有物件的 RDS 程式設計模型
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 9ce5e13641afa757f2c0ccea4ec760c4fa70b3ff
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759638"
---
# <a name="rds-programming-model-with-objects"></a>具有物件的 RDS 程式設計模型
RDS 的目標是透過像是 IIS 的媒介來取得和更新資料來源。 程式設計模型會指定完成此目標所需的活動順序。 物件模型會指定其方法和屬性會影響程式設計模型的物件。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 RDS 提供可執行下列動作順序的方法：  
  
-   指定要在伺服器上叫用的程式，並取得 (proxy) 從用戶端 (RDS 參考它的方法 [。](../../reference/rds-api/dataspace-object-rds.md)) 的空間。  
  
-   叫用伺服器程式。 將參數傳遞至識別資料來源的伺服器程式，以及要發出 (proxy 或 RDS 的命令 [。DataControl](../../reference/rds-api/datacontrol-object-rds.md)) 。  
  
-   伺服器程式會從資料來源取得 [記錄集](../../reference/ado-api/recordset-object-ado.md) 物件，通常是使用 ADO。 （選擇性）在伺服器上處理 **記錄集** 物件 ([RDSServer DataFactory](../../reference/rds-api/datafactory-object-rdsserver.md)) 。  
  
-   伺服器程式會將最終的 **記錄集** 物件傳回 (proxy) 的用戶端應用程式。  
  
-   在用戶端上，會將 **記錄集** 物件放入表單中，方便視覺控制項 (visual 控制項和 **RDS。DataControl**) 。  
  
-   對 **記錄集** 物件所做的變更會傳送回伺服器，並用來更新 RDS (的資料來源 **。DataControl** 或 **RDSServer DataFactory**) 。  
  
## <a name="see-also"></a>另請參閱  
 [RDS 物件模型摘要](./rds-object-model-summary.md)   
 [DataControl 物件 (RDS) ](../../reference/rds-api/datacontrol-object-rds.md)   
 [DataFactory 物件 (RDSServer) ](../../reference/rds-api/datafactory-object-rdsserver.md)   
 [ (RDS) 的空間物件 ](../../reference/rds-api/dataspace-object-rds.md)   
 [RDS 案例](./rds-scenario.md)   
 [RDS 教學課程](./rds-tutorial.md)   
 [ (ADO) 的記錄集物件 ](../../reference/ado-api/recordset-object-ado.md)   
 [RDS 使用方式與安全性](./rds-usage-and-security.md)