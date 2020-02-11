---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f41ef7f0641877056a6e2f3d85fd6a40ff7826db
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67925994"
---
# <a name="alternatives-using-sql-statements"></a>替代方案：使用 SQL 陳述式
ADO 也允許使用命令做為其內建屬性的替代專案，以及編輯資料的方法。 視您的提供者而定，本節所述的所有作業也可以藉由將命令傳遞至您的資料來源來達成。 例如，您可以使用 SQL UPDATE 語句來修改資料，而不需要使用**欄位**的**Value**屬性。 SQL INSERT 語句可以用來將新記錄加入至資料來源，而不是 ADO 方法**AddNew**。 如需有關 SQL 或您的提供者之資料操作語言的詳細資訊，請參閱資料來源的檔。  
  
 例如，您可以將包含 DELETE 子句的 SQL 字串傳遞至資料庫，如下列程式碼所示：  
  
```  
'BeginSQLDelete  
strSQL = "DELETE FROM Shippers WHERE ShipperID = " & intId  
objConn1.Execute strSQL, , adCmdText + adExecuteNoRecords  
'EndSQLDelete  
```
