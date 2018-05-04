---
title: setMaxRows 方法 (SQLServerStatement) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerStatement.setMaxRows
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cccc0667-589b-4655-8ea8-14ae8b2eb9dc
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 949c7a7d0b9d28c2ba14b4130db657ba357be2de
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="setmaxrows-method-sqlserverstatement"></a>setMaxRows 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  任何設定的資料列數目上限限制[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件可以包含指定的數字。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setMaxRows(int max)  
```  
  
#### <a name="parameters"></a>參數  
 *max*  
  
 **Int** ，指出資料列或 0 的最大數目，如果沒有任何限制。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 setMaxRows 方法是由 java.sql.Statement 介面中的 setMaxRows 方法指定。  
  
 此 setMaxRows 方法沒有任何作用動態的可捲動資料指標。 應用程式應該要使用 SELECT TOP N SQL 語法，限制可能的大型結果集傳回的資料列數。  
  
 SetMaxRows 方法呼叫時，[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]執行應用程式的查詢時執行 SET ROWCOUNT SQL 陳述式。 這會導致 JDBC 驅動程式限制受到所有資料列的數目上限[!INCLUDE[tsql](../../../includes/tsql_md.md)]陳述式，該查詢中，執行查詢所傳回的不只是資料列數目。 如果應用程式需要來限制只在最上層[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件時，它應該使用 SELECT TOP N SQL 語法，在查詢中，而不是 setMaxRows 方法。  
  
 如需有關 SET ROWCOUNT SQL 陳述式的詳細資訊，請參閱 「[SET ROWCOUNT (TRANSACT-SQL)](http://go.microsoft.com/fwlink/?LinkId=139522)」 中的主題[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]線上叢書 》。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
