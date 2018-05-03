---
title: 替代方案： 使用 SQL 陳述式 |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ADO]
- editing data [ADO], sql statements
- ADO, SQL statements
ms.assetid: 8b528b23-063d-45ea-8dea-6a90d4060b20
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 09f2220a4dc896858923013a087d5e52c373809f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="alternatives-using-sql-statements"></a>替代方案： 使用 SQL 陳述式
ADO 也可以使用命令做為內建屬性和方法，來編輯資料的替代項目。 根據您的提供者，這一節所述的所有作業也都可藉由將命令傳遞至您的資料來源。 例如，SQL UPDATE 陳述式可用來修改資料而不使用**值**屬性**欄位**。 SQL INSERT 陳述式可用來將新記錄新增至資料來源，而不是 ADO 方法**AddNew**。 如需有關 SQL 或您的提供者的資料操作語言的詳細資訊，請參閱資料來源的文件。  
  
 例如，您可以傳遞 SQL 字串，包含資料庫，DELETE 陳述式，如下列程式碼所示：  
  
```  
'BeginSQLDelete  
strSQL = "DELETE FROM Shippers WHERE ShipperID = " & intId  
objConn1.Execute strSQL, , adCmdText + adExecuteNoRecords  
'EndSQLDelete  
```
