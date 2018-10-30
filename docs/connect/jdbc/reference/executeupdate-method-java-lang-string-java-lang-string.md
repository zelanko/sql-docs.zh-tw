---
title: executeUpdate 方法 (java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.executeUpdate (java.lang.String[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2f44a689-65c8-4c94-9574-e9c08ea7918e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 83e035d659fd7b6b59c7b8d8a0799415bef5c112
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47611704"
---
# <a name="executeupdate-method-javalangstring-javalangstring"></a>executeUpdate 方法 (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  執行指定的 SQL 陳述式，並向 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 發出信號，通知必須提供在指定陣列中所指出的自動產生索引鍵以進行擷取。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final int executeUpdate(java.lang.String sql,  
                               java.lang.String[] columnNames)  
```  
  
#### <a name="parameters"></a>參數  
 *sql*  
  
 包含 SQL 陳述式的**字串**。  
  
 *columnNames*  
  
 **String** 類型的陣列，指出必須提供自動產生索引鍵的資料行名稱。  
  
## <a name="return-value"></a>傳回值  
 **int**，指出受影響的資料列數目，如果是使用 DDL 陳述式，則為 0。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 executeUpdate 方法是由 java.sql.Statement 介面中的 executeUpdate 方法指定。  
  
 如果執行預存程序產生的更新計數大於一或是產生一個以上的結果集，請使用 [execute](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md) 方法執行預存程序。  
  
## <a name="see-also"></a>另請參閱  
 [executeUpdate 方法 &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)   
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
