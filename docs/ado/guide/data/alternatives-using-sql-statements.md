---
description: 替代方案：使用 SQL 陳述式
title: 替代方案：使用 SQL 語句 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ADO]
- editing data [ADO], sql statements
- ADO, SQL statements
ms.assetid: 8b528b23-063d-45ea-8dea-6a90d4060b20
author: rothja
ms.author: jroth
ms.openlocfilehash: f71afb691aa170910e93f73ac539e1b69a691bca
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453740"
---
# <a name="alternatives-using-sql-statements"></a>替代方案：使用 SQL 陳述式
ADO 也可讓您使用命令做為其內建屬性和方法的替代專案，以編輯資料。 視您的提供者而定，本節中提及的所有作業也可以藉由將命令傳遞至您的資料來源來達成。 例如，您可以使用 SQL UPDATE 語句來修改資料，而不需要使用**欄位**的**Value**屬性。 您可以使用 SQL INSERT 語句，將新的記錄新增至資料來源，而不是 ADO 方法的 **AddNew**。 如需有關 SQL 或您提供者之資料操作語言的詳細資訊，請參閱您資料來源的檔。  
  
 例如，您可以將包含 DELETE 子句的 SQL 字串傳遞至資料庫，如下列程式碼所示：  
  
```  
'BeginSQLDelete  
strSQL = "DELETE FROM Shippers WHERE ShipperID = " & intId  
objConn1.Execute strSQL, , adCmdText + adExecuteNoRecords  
'EndSQLDelete  
```
