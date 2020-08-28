---
description: RDS 屬性
title: RDS 屬性 |Microsoft Docs
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
helpviewer_keywords:
- RDS properties [ADO]
- properties [ADO], RDS
ms.assetid: e4e04cbd-21fc-44a1-9f21-49aa68746934
author: rothja
ms.author: jroth
ms.openlocfilehash: a4f47967fc80ba488c57299fe7f94c13d9f9e949
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88981519"
---
# <a name="rds-properties"></a>RDS 屬性
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
|屬性|描述|  
|-|-|  
|[連接 (RDS) ](./connect-property-rds.md)|指出執行查詢和更新作業的資料庫名稱。|  
|[ExecuteOptions (RDS) ](./executeoptions-property-rds.md)|指出是否已啟用非同步執行。|  
|[FetchOptions (RDS) ](./fetchoptions-property-rds.md)|表示非同步提取的型別。|  
|[FilterColumn (RDS) ](./filtercolumn-property-rds.md)|表示用來評估篩選準則的資料行。|  
|[FilterCriterion (RDS) ](./filtercriterion-property-rds.md)|表示要在篩選值中使用的評估運算子。|  
|[FilterValue (RDS) ](./filtervalue-property-rds.md)|指出篩選記錄的值。|  
|[ (RDS) 的處理常式 ](./handler-property-rds.md)|指出伺服器端自訂程式的名稱， (*處理常式*) 擴充 **RDSServer. DataFactory**的功能，以及 *處理常式*所使用的任何參數。|  
|[InternetTimeout (RDS) ](./internettimeout-property-rds.md)|表示要求超時前等待的毫秒數。|  
|[ReadyState (RDS) ](./readystate-property-rds.md)|表示 **DataControl** 物件在其 **記錄集** 物件中提取資料時的進度。|  
|[記錄集和 SourceRecordset (RDS) ](./recordset-sourcerecordset-properties-rds.md)|表示從自訂商務物件傳回的 **記錄集** 物件。|  
|[Server (RDS) ](./server-property-rds.md)|指出 Internet Information Services (IIS) 名稱和通訊協定。|  
|[SortColumn (RDS) ](./sortcolumn-property-rds.md)|指出排序記錄的資料行。|  
|[SortDirection (RDS) ](./sortdirection-property-rds.md)|指出排序次序為遞增或遞減。|  
|[SQL (RDS) ](./sql-property.md)|表示用來取出 **記錄集**的查詢字串。|  
|[RDS)  (URL ](./url-property-rds.md)|指出包含相對或絕對 URL 的字串。|