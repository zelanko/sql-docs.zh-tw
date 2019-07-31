---
title: 資料成形所需的提供者 |Microsoft Docs
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
ms.openlocfilehash: 732563fc2c4e1cc93beac8712d845b960ae56aaf
ms.sourcegitcommit: 97e94b76f9f48d161798afcf89a8c2ac0f09c584
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/30/2019
ms.locfileid: "68661271"
---
# <a name="required-providers-for-data-shaping"></a>資料成形所需的提供者
資料成形通常需要兩個提供者。 服務提供者、[適用于 OLE DB 的資料成形服務](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)會提供資料成形功能, 而資料提供者 (例如 SQL Server 的 OLE DB 提供者) 會提供資料列來填入已塑造的[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
 服務提供者的名稱 (MSDataShape) 可以指定為[connection](../../../ado/reference/ado-api/connection-object-ado.md)物件[提供者](../../../ado/reference/ado-api/provider-property-ado.md)屬性的值, 或連接字串關鍵字 "provider = MSDataShape;"。  
  
 您可以將資料提供者的名稱指定為**Data Provider**動態屬性的值, 這會由 OLE DB 的資料成形服務或連接字串關鍵字加入至**連接**物件[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合中。**Data Provider =** _提供者_」。  
  
 如果未填入**記錄集**, 則不需要任何資料提供者 (例如, 如同在使用 NEW 關鍵字建立資料行的製造**記錄集**內)。 在此情況下, 請指定 "**Data Provider =** none;"。  
  
## <a name="example"></a>範例  
  
```  
Dim cnn As New ADODB.Connection  
cnn.Provider = "MSDataShape"  
cnn.Open "Data Provider=SQLOLEDB;Integrated Security=SSPI;Database=Northwind"  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](../../../ado/guide/data/data-shaping-example.md)   
 [正式圖形文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [一般 Shape 命令](../../../ado/guide/data/shape-commands-in-general.md)
