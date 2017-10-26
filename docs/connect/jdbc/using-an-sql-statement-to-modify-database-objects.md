---
title: "使用 SQL 陳述式來修改資料庫物件 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f49ea499-df3c-4e85-9fc7-450fb99622a6
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d5b94ff83ef6cea934efb66f6efb9394d2fa2501
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

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
 [使用 SQL 陳述式](../../connect/jdbc/using-statements-with-sql.md)  
  
  

