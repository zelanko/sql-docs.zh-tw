---
title: "替代方案： 使用 SQL 陳述式 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ADO]
- editing data [ADO], sql statements
- ADO, SQL statements
ms.assetid: 8b528b23-063d-45ea-8dea-6a90d4060b20
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 85831e635103ec622414af7a77d545fb470c3f7e
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
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
