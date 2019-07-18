---
title: 資料來源屬性 (ADO) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fd677e29631e53eeb71c43e8174baff553defc85
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933242"
---
# <a name="datasource-property-ado"></a>DataSource 屬性 (ADO)
表示包含資料表示為物件[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。  
  
## <a name="remarks"></a>備註  
 這個屬性用來與資料環境中建立資料繫結控制項。 資料環境維護集合包含的資料 （資料來源） 為具名物件 （資料成員），將會呈現為**資料錄集**物件。  
  
 [DataMember](../../../ado/reference/ado-api/datamember-property.md)並**DataSource**屬性必須搭配使用。  
  
 參考的物件必須實作**IDataSource**介面，並必須包含**IRowset**介面。  
  
## <a name="usage"></a>使用量  
  
```  
Dim rs as New ADODB.Recordset  
rs.DataMember = "Command"     'Name of the rowset to bind to.  
Set rs.DataSource = myDE      'Name of the object containing an IRowset.  
```  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [DataMember 屬性](../../../ado/reference/ado-api/datamember-property.md)
