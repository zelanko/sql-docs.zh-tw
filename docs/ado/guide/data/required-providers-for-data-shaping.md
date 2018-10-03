---
title: 資料成形所需提供者 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], data shaping
- data shaping [ADO], providers required
ms.assetid: d49d48d2-ac2d-4c11-895c-5a149b444620
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 482139f8aa3dc42bbd17593b58fcc8510f1fc9a8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47713836"
---
# <a name="required-providers-for-data-shaping"></a>資料成形所需的提供者
資料成形時，通常會需要兩個提供者。 服務提供者[OLE db Data Shaping Service](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)提供的資料成形功能，並為資料提供者，例如 OLE DB Provider for SQL Server，提供資料列的資料來填入形狀[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
 服務提供者 (MSDataShape) 的名稱可以指定的值為[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件[提供者](../../../ado/reference/ado-api/provider-property-ado.md)屬性或連接字串關鍵字"Provider = MSDataShape; 」。  
  
 資料提供者的名稱可以指定的值為**資料提供者**動態屬性，它會新增至**連線**物件[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合Data Shaping Service 的 OLE DB 或連接字串關鍵字 」 **資料提供者 = * * * 提供者*"。  
  
 如果任何資料提供者，則需要**資料錄集**不會擴展 (例如，就像製作**資料錄集**會建立資料行使用新的關鍵字)。 在此情況下，指定 「**資料提供者 =** none;"。  
  
## <a name="example"></a>範例  
  
```  
Dim cnn As New ADODB.Connection  
cnn.Provider = "MSDataShape"  
cnn.Open "Data Provider=SQLOLEDB;Integrated Security=SSPI;Database=Northwind"  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](../../../ado/guide/data/data-shaping-example.md)   
 [正式 Shape 文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [一般 Shape 命令](../../../ado/guide/data/shape-commands-in-general.md)
