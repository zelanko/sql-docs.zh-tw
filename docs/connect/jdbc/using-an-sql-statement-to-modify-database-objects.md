---
title: 使用 SQL 陳述式修改資料庫物件 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f49ea499-df3c-4e85-9fc7-450fb99622a6
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b126fb0b5a72688c1801cf8854d8035763c8245f
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38040576"
---
# <a name="using-an-sql-statement-to-modify-database-objects"></a>使用 SQL 陳述式修改資料庫物件
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  若要使用 SQL 陳述式修改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 資料庫物件，您可使用 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 類別的 [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md) 方法。 executeUpdate 方法會將 SQL 陳述式傳遞至資料庫以進行處理，然後由於沒有任何資料列受影響而傳回 0 值。  
  
 若要這樣做，您必須先使用 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 類別的 [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) 方法建立 SQLServerStatement 物件。  
  
> [!NOTE]  
>  在資料庫內修改物件的 SQL 陳述式稱為資料定義語言 (DDL) 陳述式。 這些陳述式包含 CREATE TABLE、DROP TABLE、CREATE INDEX 及 DROP INDEX 等陳述式。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 所支援之DDL 陳述式類型的詳細資訊，請參閱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 線上叢書。  
  
 在下列範例中，[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 範例資料庫的開啟連線會傳入至函式、建構會在資料庫中建立簡易 TestTable 的 SQL 陳述式，然後執行陳述式並顯示傳回值。  
  
 [!code[JDBC#UsingSQLToModifyDBObjects1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-t_0_1.java)]  
  
## <a name="see-also"></a>另請參閱  
 [搭配使用陳述式與 SQL](../../connect/jdbc/using-statements-with-sql.md)  
  
  
