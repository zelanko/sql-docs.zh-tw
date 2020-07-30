---
title: ADO 動態屬性 |Microsoft Docs
ms.prod: sql
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- dynamic properties [ADO]
- properties [ADO], dynamic
ms.assetid: d7b06d72-f792-4328-93a2-5006b9e2c581
author: rothja
ms.author: jroth
ms.openlocfilehash: c727f73abed5fe9a30ebf191e2c6da60f8baa13a
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242888"
---
# <a name="ado-dynamic-properties"></a>ADO 動態屬性
動態屬性可以加入至[Connection](../../../ado/reference/ado-api/connection-object-ado.md)、 [Command](../../../ado/reference/ado-api/command-object-ado.md)或[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)物件的[properties](../../../ado/reference/ado-api/properties-collection-ado.md)集合中。 這些屬性的來源是資料提供者，例如[SQL Server 的 OLE DB 提供者](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)，或是服務提供者（例如[OLE DB 的 Microsoft Cursor 服務](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)）。 如需特定動態屬性的詳細資訊，請參閱適當的資料提供者或服務提供者檔。  
  
 [Ado 動態屬性索引](../../../ado/reference/ado-api/ado-dynamic-property-index.md)會提供每個標準 OLE DB 提供者動態屬性的 ado 和 OLE DB 名稱之間的交互參考。  
  
 下列動態屬性特別有趣，而且也記載于先前所述的來源中。 使用 ADO 的特殊功能記載于下列清單中的 ADO 說明主題。  
  
|動態屬性|描述|  
|-|-|  
|[最佳化](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)|指定是否應該在此欄位上建立索引。|  
|[提示](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)|指定 OLE DB 提供者是否應該提示使用者提供初始化資訊。|  
|[重新調整名稱](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)|指定**記錄集**物件的名稱。|  
|[重新同步命令](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)|指定使用者提供的命令字串，重新**同步**處理方法會發出此錯誤，以重新整理**唯一資料表**動態屬性中名為的資料表中的資料。|  
|[唯一的資料表、唯一的架構、唯一的目錄](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|**唯一資料表**指定允許更新、插入和刪除的基表名稱。<br /><br /> **唯一的架構**指定資料表的架構或擁有者的名稱。<br /><br /> **唯一目錄**指定包含資料表的目錄或資料庫名稱。|  
|[更新重新同步](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)|指定**UpdateBatch**方法後面是否接著隱含的重新**同步**處理方法作業，如果是，則為該作業的範圍。|
| &nbsp; | &nbsp; |

## <a name="see-also"></a>另請參閱  
 [ADO API 參考](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO 集合](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO 列舉常數](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [附錄 B： ADO 錯誤](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [ADO 事件](../../../ado/reference/ado-api/ado-events.md)   
 [ADO 方法](../../../ado/reference/ado-api/ado-methods.md)   
 [ADO 物件模型](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO 物件和介面](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [ADO 屬性](../../../ado/reference/ado-api/ado-properties.md)
