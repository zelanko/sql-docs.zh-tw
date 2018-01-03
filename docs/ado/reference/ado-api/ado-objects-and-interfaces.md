---
title: "ADO 物件與介面 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ADO, objects and interfaces
- objects [ADO]
ms.assetid: d0b7e254-c89f-4406-b846-a060ef038c30
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ad14c7327d3dc7186ff86c3ca0ba84d206143973
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="ado-objects-and-interfaces"></a>ADO 物件與介面
以表示這些物件之間的關聯性[ADO 物件模型](../../../ado/reference/ado-api/ado-object-model.md)。  
  
 每個物件可以包含在其對應的集合。 例如，[錯誤](../../../ado/reference/ado-api/error-object.md)物件可以包含在[錯誤](../../../ado/reference/ado-api/errors-collection-ado.md)集合。 如需詳細資訊，請參閱[ADO 集合](../../../ado/reference/ado-api/ado-collections.md)或特定集合的主題。  
  
|||  
|-|-|  
|[IADOCommandConstruction](https://msdn.microsoft.com/library/windows/desktop/aa965677.aspx)|用來擷取基礎 OLEDB 命令從 ADOCommand 物件。|  
|[ADORecordConstruction](../../../ado/reference/ado-api/adorecordconstruction-interface.md)|建構 ADO**記錄**從 OLE DB 物件**列**C/c + + 應用程式中的物件。|  
|[ADORecordsetConstruction](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)|建構 ADO**資料錄集**從 OLE DB 物件**資料列集**C/c + + 應用程式中的物件。|  
|[ADOStreamConstruction 介面](../../../ado/reference/ado-api/adostreamconstruction-interface.md)|建構 ADO**資料流**從 OLE DB 物件**IStream** C/c + + 應用程式中的物件。|  
|[Command](../../../ado/reference/ado-api/command-object-ado.md)|定義您想要執行對資料來源的特定命令。<br /><br /> **命令**物件不是安全的。|  
|[[連接]](../../../ado/reference/ado-api/connection-object-ado.md)|代表資料來源的開啟連接。<br /><br /> **連接**物件而言是安全的指令碼。|  
|[IDSOShapeExtensions 介面](../../../ado/reference/ado-api/idsoshapeextensions-interface.md)|SHAPE 提供者取得基礎 OLEDB 資料來源物件。|  
|[錯誤](../../../ado/reference/ado-api/error-object.md)|包含關於涉及提供者的單一作業相關的資料存取錯誤的詳細資料。<br /><br /> **錯誤**物件不是安全的。|  
|[欄位](../../../ado/reference/ado-api/field-object.md)|代表具有通用的資料類型的資料行。|  
|[參數](../../../ado/reference/ado-api/parameter-object.md)|代表參數或相關聯的引數**命令**物件會根據參數型的查詢或預存程序。<br /><br /> **參數**物件不是安全的。|  
|[屬性](../../../ado/reference/ado-api/property-object-ado.md)|代表動態 ADO 物件提供者所定義的特性。|  
|[資料錄](../../../ado/reference/ado-api/record-object-ado.md)|代表的一列**資料錄集**、 目錄或檔案系統中的檔案。 **記錄**物件而言是安全的指令碼。|  
|[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)|代表一組記錄的基底資料表或執行的命令的結果。 在任何時候，**資料錄集**物件是指單一資料錄和目前的記錄集內。<br /><br /> **資料錄集**物件而言是安全的指令碼。|  
|[資料流](../../../ado/reference/ado-api/stream-object-ado.md)|代表二進位資料流的資料。<br /><br /> **資料流**物件而言是安全的指令碼。|  
  
## <a name="see-also"></a>請參閱  
 [ADO 應用程式開發介面參考](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO 集合](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO 動態屬性](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [ADO 列舉常數](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [附錄 b: ADO 錯誤](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [ADO 事件](../../../ado/reference/ado-api/ado-events.md)   
 [ADO 方法](../../../ado/reference/ado-api/ado-methods.md)   
 [ADO 物件模型](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO 屬性](../../../ado/reference/ado-api/ado-properties.md)
