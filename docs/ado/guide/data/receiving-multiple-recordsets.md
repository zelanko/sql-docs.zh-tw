---
title: 接收多個資料錄集 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- receiving multiple Recordsets [ADO]
- Recordset object [ADO], receiving multiple Recordsets
ms.assetid: 2a7ad7a6-f00d-4355-b0b5-d0ab957b0566
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6d6e649201b8bf23a1b696d574baea2f4b049e06
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924536"
---
# <a name="receiving-multiple-recordsets"></a>接收多個資料錄集
[Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)支援傳回多個**Recordset**物件的單一命令，其中包含多個 SQL 陳述式，一個**資料錄集**每個 SQL 陳述式。 順序**資料錄集**會傳回如下的 SQL 陳述式會置於命令文字的順序。  
  
 當命令包含 COMPUTE 子句時，Microsoft OLE DB Provider for SQL Server 會將多個結果集也傳回 ado。 例如，包含下列 SQL 陳述式的命令時，會在兩個傳回的結果**資料錄集**物件： 一個用於資料列集 (*ProductID*， *ProductName*，*UnitPrice*)，和另一個則用於在資料表中的所有產品的平均價格。  
  
```  
SELECT ProductID, ProductName, UnitPrice   
  FROM PRODUCTS   
  COMPUTE AVG(UnitPrice)  
```  
  
 您可以使用**Recordset.NextRecordset**来列舉的兩個物件的方法。  
  
 如需詳細資訊，請參閱 < [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)。
