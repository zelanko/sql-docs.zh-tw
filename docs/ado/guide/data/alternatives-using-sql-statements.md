---
title: 替代方案： 使用 SQL 陳述式 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b95e6f0bd2b702080b3580b8b9eeb80ac5b06e8d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47674256"
---
# <a name="alternatives-using-sql-statements"></a>替代方案：使用 SQL 陳述式
ADO 也可讓使用命令作為其內建的屬性和方法，來編輯資料的替代方案。 視您的提供者而定，這一節所述的所有作業也都可藉由將命令傳遞至您的資料來源。 例如，SQL UPDATE 陳述式可用來修改資料，而不使用**值**屬性**欄位**。 SQL INSERT 陳述式可用來將新記錄新增至資料來源，而不是 ADO 方法**AddNew**。 如需 SQL 或您的提供者的資料操作語言的詳細資訊，請參閱您的資料來源的文件。  
  
 例如，您可以傳遞 SQL 字串，包含資料庫，DELETE 陳述式，如下列程式碼所示：  
  
```  
'BeginSQLDelete  
strSQL = "DELETE FROM Shippers WHERE ShipperID = " & intId  
objConn1.Execute strSQL, , adCmdText + adExecuteNoRecords  
'EndSQLDelete  
```
