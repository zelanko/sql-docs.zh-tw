---
title: "所需資料成形的提供者 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- providers [ADO], data shaping
- data shaping [ADO], providers required
ms.assetid: d49d48d2-ac2d-4c11-895c-5a149b444620
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c2dc7048ea3442a77f6aadf7d7b1868c2ac9d833
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="required-providers-for-data-shaping"></a>提供者所需的資料成形
資料成形時，通常會需要兩個提供者。 服務提供者[for OLE DB Data Shaping Service](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)、 提供用來形成功能和資料提供者，例如 SQL Server 的 OLE DB 提供者的資料、 提供資料列的資料來填入形狀[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
 名稱服務提供者 (MSDataShape) 可以指定的值為[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件[提供者](../../../ado/reference/ado-api/provider-property-ado.md)屬性或連接字串關鍵字 」 提供者 = MSDataShape;"。  
  
 資料提供者的名稱可以指定的值為**資料提供者**動態屬性，它會加入**連接**物件[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合Data Shaping Service 的 OLE DB 或連接字串關鍵字"**資料提供者 =***提供者*"。  
  
 如果任何資料提供者，則需要**資料錄集**不會擴展 (例如，就像優質**資料錄集**會建立資料行與新的關鍵字)。 在此情況下，指定 「**資料提供者 =**none;"。  
  
## <a name="example"></a>範例  
  
```  
Dim cnn As New ADODB.Connection  
cnn.Provider = "MSDataShape"  
cnn.Open "Data Provider=SQLOLEDB;Integrated Security=SSPI;Database=Northwind"  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](../../../ado/guide/data/data-shaping-example.md)   
 [型式圖形文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [在一般的圖形命令](../../../ado/guide/data/shape-commands-in-general.md)

