---
description: 接收多個資料錄集
title: 接收多個記錄集 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: d5aad021e1d6003ba3c8d30915f1648f57124984
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453010"
---
# <a name="receiving-multiple-recordsets"></a>接收多個資料錄集
[適用于 SQL Server 的 Microsoft OLE DB 提供者](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)支援針對包含多個 sql 語句的單一命令，傳回多個**記錄集**物件，每個 Sql 語句一個**記錄集**。 **記錄集**傳回的順序會遵循 SQL 語句放在命令文字中的順序。  
  
 當命令包含 COMPUTE 子句時，適用于 SQL Server 的 Microsoft OLE DB 提供者也會將多個結果集傳回給 ADO。 例如，包含下列 SQL 語句的命令將會在兩個 **記錄集** 物件中傳回結果：一個適用于 (*ProductID*、 *ProductName*、price) 的資料列 *集，另* 一個則是資料表中所有產品的平均價格。  
  
```  
SELECT ProductID, ProductName, UnitPrice   
  FROM PRODUCTS   
  COMPUTE AVG(UnitPrice)  
```  
  
 您可以使用 **NextRecordset** 方法來列舉這兩個物件。  
  
 如需詳細資訊，請參閱 [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)。
