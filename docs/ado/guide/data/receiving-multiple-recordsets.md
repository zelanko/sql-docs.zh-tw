---
title: "接收多個資料錄集 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- receiving multiple Recordsets [ADO]
- Recordset object [ADO], receiving multiple Recordsets
ms.assetid: 2a7ad7a6-f00d-4355-b0b5-d0ab957b0566
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3687e3ee6a2588a5461e48a1f3f26db91d14a8fb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="receiving-multiple-recordsets"></a>接收多個資料錄集
[Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)支援傳回多個**資料錄集**物件單一命令，其中包含多個 SQL 陳述式，一個**資料錄集**每個 SQL 陳述式。 順序**資料錄集**會傳回遵照 SQL 陳述式會置於命令文字的順序。  
  
 Microsoft OLE DB Provider for SQL Server 也會傳回多個結果集至 ADO 當命令包含 COMPUTE 子句。 比方說，包含下列 SQL 陳述式的命令時，會在兩個傳回的結果**資料錄集**物件： 一個用於資料列集 (*ProductID*， *ProductName*，*UnitPrice*)，和另一個則用於資料表中的所有產品的平均價格。  
  
```  
SELECT ProductID, ProductName, UnitPrice   
  FROM PRODUCTS   
  COMPUTE AVG(UnitPrice)  
```  
  
 您可以使用**Recordset.NextRecordset**方法來列舉將兩個物件。  
  
 如需詳細資訊，請參閱[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)。
