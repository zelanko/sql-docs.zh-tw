---
title: 使用 SQL 陳述式來修改資料庫物件 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f49ea499-df3c-4e85-9fc7-450fb99622a6
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6bb291d725728ef7d5e87f0331f14aac33b19ba8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="using-an-sql-statement-to-modify-database-objects"></a>使用 SQL 陳述式修改資料庫物件
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  若要修改[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]使用的 SQL 陳述式的資料庫物件，您可以使用[executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)方法[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)類別。 ExecuteUpdate 方法會將 SQL 陳述式傳遞至資料庫以進行處理，，，然後傳回值為 0，因為沒有資料列受到影響。  
  
 若要這樣做，您必須先建立 SQLServerStatement 物件使用[createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)方法[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)類別。  
  
> [!NOTE]  
>  在資料庫內修改物件的 SQL 陳述式稱為資料定義語言 (DDL) 陳述式。 這些陳述式包含 CREATE TABLE、DROP TABLE、CREATE INDEX 及 DROP INDEX 等陳述式。 如需有關所支援的 DDL 陳述式的型別[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，請參閱[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]線上叢書 》。  
  
 在下列範例中，開啟連接[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]範例資料庫會傳遞至函式、 建構 SQL 陳述式會建立簡易 TestTable 在資料庫中，然後執行陳述式並顯示傳回的值。  
  
 [!code[JDBC#UsingSQLToModifyDBObjects1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-t_0_1.java)]  
  
## <a name="see-also"></a>另請參閱  
 [搭配使用陳述式與 SQL](../../connect/jdbc/using-statements-with-sql.md)  
  
  
