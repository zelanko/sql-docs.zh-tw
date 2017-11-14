---
title: "ADO 動態屬性 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dynamic properties [ADO]
- properties [ADO], dynamic
ms.assetid: d7b06d72-f792-4328-93a2-5006b9e2c581
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fca9f032f5a72df58b18206c8441365ce3c8a746
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="ado-dynamic-properties"></a>ADO 動態屬性
動態屬性可以加入至[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合[連接](../../../ado/reference/ado-api/connection-object-ado.md)，[命令](../../../ado/reference/ado-api/command-object-ado.md)，或[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。 這些屬性的來源是具備資料提供者，例如[OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)，或服務提供者，例如[Microsoft OLE DB 的資料指標服務](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)。 請參閱適當的資料提供者或服務提供者文件，如需有關特定的動態屬性。  
  
 [ADO 動態屬性索引](../../../ado/reference/ado-api/ado-dynamic-property-index.md)提供 ADO 和 OLE DB 的每個標準 OLE DB 提供者動態屬性名稱之間的交互參考。  
  
 下列的動態屬性特別有趣，而且也會記錄在先前提到的來源。 ADO 說明主題，下列清單中會詳細說明使用 ADO 的特殊功能。  
  
|||  
|-|-|  
|[最佳化](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)|指定是否應該在此欄位上建立索引。|  
|[提示](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)|指定的 OLE DB 提供者是否應提示使用者輸入的初始化資訊。|  
|[重繪名稱](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)|指定的名稱**資料錄集**物件。|  
|[重新同步處理命令](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)|指定使用者提供的命令字串**重新同步處理**方法問題中名為資料表中的資料重新整理**唯一資料表**動態屬性。|  
|[唯一資料表、 唯一的結構描述、 唯一的目錄](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|**唯一資料表**指定基底資料表的更新、 插入和刪除允許的名稱。<br /><br /> **唯一的結構描述**指定結構描述或資料表的擁有者的名稱。<br /><br /> **唯一的目錄**指定的目錄或資料庫包含之資料表的名稱。|  
|[更新的重新同步處理](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)|指定是否**UpdateBatch**方法後面的隱含**重新同步處理**方法作業，而且如果是，該作業的範圍。|  
  
## <a name="see-also"></a>另請參閱  
 [ADO 應用程式開發介面參考](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO 集合](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO 列舉常數](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [附錄 b: ADO 錯誤](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [ADO 事件](../../../ado/reference/ado-api/ado-events.md)   
 [ADO 方法](../../../ado/reference/ado-api/ado-methods.md)   
 [ADO 物件模型](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO 物件與介面](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [ADO 屬性](../../../ado/reference/ado-api/ado-properties.md)

