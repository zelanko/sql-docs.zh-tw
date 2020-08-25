---
description: ADO 動態屬性
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
ms.openlocfilehash: 83ab2320d3400c5be066af246b50daccaf468462
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88771757"
---
# <a name="ado-dynamic-properties"></a>ADO 動態屬性
動態屬性可以加入至[連接](./connection-object-ado.md)、[命令](./command-object-ado.md)或[記錄集](./recordset-object-ado.md)物件的[屬性](./properties-collection-ado.md)集合。 這些屬性的來源是資料提供者，例如 [SQL Server 的 OLE DB 提供者](../../guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)，或是服務提供者（例如 [OLE DB 的 Microsoft 資料指標服務](../../guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)）。 如需特定動態屬性的詳細資訊，請參閱適當的資料提供者或服務提供者檔。  
  
 [Ado 動態屬性索引](./ado-dynamic-property-index.md)提供每個標準 OLE DB 提供者動態屬性的 ado 和 OLE DB 名稱之間的交互參考。  
  
 下列動態屬性特別有趣，而且也記載于稍早所述的來源中。 ADO 的特殊功能記載于下列清單中的 ADO 說明主題。  
  
|動態屬性|描述|  
|-|-|  
|[最佳化](./optimize-property-dynamic-ado.md)|指定是否應該在此欄位上建立索引。|  
|[提示](./prompt-property-dynamic-ado.md)|指定 OLE DB 提供者是否應該提示使用者提供初始化資訊。|  
|[重新調整名稱](./reshape-name-property-dynamic-ado.md)|指定 **記錄集** 物件的名稱。|  
|[Resync 命令](./resync-command-property-dynamic-ado.md)|指定使用者提供的命令字串，重新 **同步** 處理方法會發出重新整理，以重新整理 **Unique table** 動態屬性中所指定資料表中的資料。|  
|[唯一資料表、唯一架構、唯一目錄](./unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|**唯一資料表** 指定允許更新、插入和刪除的基表名稱。<br /><br /> **唯一架構** 指定資料表的架構或擁有者名稱。<br /><br /> **唯一目錄** 指定包含資料表的目錄或資料庫名稱。|  
|[更新重新同步](./update-resync-property-dynamic-ado.md)|指定 **UpdateBatch** 方法後面是否接著隱含的 **Resync** 方法作業，如果是，則為該作業的範圍。|
| &nbsp; | &nbsp; |

## <a name="see-also"></a>另請參閱  
 [ADO API 參考](./ado-api-reference.md)   
 [ADO 集合](./ado-collections.md)   
 [ADO 列舉常數](./ado-enumerated-constants.md)   
 [附錄 B： ADO 錯誤](../../guide/appendixes/appendix-b-ado-errors.md)   
 [ADO 事件](./ado-events.md)   
 [ADO 方法](./ado-methods.md)   
 [ADO 物件模型](./ado-object-model.md)   
 [ADO 物件和介面](./ado-objects-and-interfaces.md)   
 [ADO 屬性](./ado-properties.md)