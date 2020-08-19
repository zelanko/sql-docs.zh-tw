---
description: DataSource 屬性 (ADO)
title: DataSource 屬性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::DataSource
helpviewer_keywords:
- DataSource property [ADO]
ms.assetid: 300a702a-3544-48c5-b759-83b511fe97e0
author: rothja
ms.author: jroth
ms.openlocfilehash: 8b85f163ddb3f1fc31116966127bc01efa17a262
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444220"
---
# <a name="datasource-property-ado"></a>DataSource 屬性 (ADO)
表示物件，該物件包含要表示為 [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md) 物件的資料。  
  
## <a name="remarks"></a>備註  
 這個屬性是用來建立資料繫結控制項與資料環境。 資料環境會維護資料 (資料來源的集合，) 包含命名物件 (資料成員) 將表示為 **記錄集** 物件。  
  
 [DataMember](../../../ado/reference/ado-api/datamember-property.md)和**DataSource**屬性必須一起使用。  
  
 參考的物件必須執行 **IDataSource** 介面，且必須包含 **IRowset** 介面。  
  
## <a name="usage"></a>使用量  
  
```  
Dim rs as New ADODB.Recordset  
rs.DataMember = "Command"     'Name of the rowset to bind to.  
Set rs.DataSource = myDE      'Name of the object containing an IRowset.  
```  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [DataMember 屬性](../../../ado/reference/ado-api/datamember-property.md)
