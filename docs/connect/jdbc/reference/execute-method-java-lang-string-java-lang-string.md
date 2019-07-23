---
title: execute 方法 (java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.execute (java.lang.String.java.lang.String[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9451c7c2-4c0d-4d1e-9b42-a26ff28e3f6a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e93875cfc18ed3992fd1680a0c948e38a31f998e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67954970"
---
# <a name="execute-method-javalangstring-javalangstring"></a>execute 方法 (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  執行可傳回多個結果的指定 SQL 陳述式，並向 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 發出訊號，通知必須提供指定陣列所指出的自動產生索引鍵以進行擷取。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final boolean execute(java.lang.String sql,  
                             java.lang.String[] columnNames)  
```  
  
#### <a name="parameters"></a>參數  
 *sql*  
  
 包含 SQL 陳述式的**字串**。  
  
 *columnNames*  
  
 字串的陣列，這些字串會指出必須提供自動產生索引鍵的資料行名稱。  
  
## <a name="return-value"></a>傳回值  
 如果第一個結果是結果集，則為 **true** 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 execute 方法是由 java.sql.Statement 介面中的 execute 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [執行方法&#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md)   
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
