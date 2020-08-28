---
description: DataSource 屬性 (ADO)
title: DataSource 屬性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 48c5969df864364cd87d131fce2740a5a0e043f7
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974259"
---
# <a name="datasource-property-ado"></a>DataSource 屬性 (ADO)
表示物件，該物件包含要表示為 [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md) 物件的資料。  
  
## <a name="remarks"></a>備註  
 這個屬性是用來建立資料繫結控制項與資料環境。 資料環境會維護資料 (資料來源的集合，) 包含命名物件 (資料成員) 將表示為 **記錄集** 物件。  
  
 [DataMember](../../../ado/reference/ado-api/datamember-property.md)和**DataSource**屬性必須一起使用。  
  
 參考的物件必須執行 **IDataSource** 介面，且必須包含 **IRowset** 介面。  
  
## <a name="usage"></a>使用方式  
  
```  
Dim rs as New ADODB.Recordset  
rs.DataMember = "Command"     'Name of the rowset to bind to.  
Set rs.DataSource = myDE      'Name of the object containing an IRowset.  
```  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [DataMember 屬性](../../../ado/reference/ado-api/datamember-property.md)
