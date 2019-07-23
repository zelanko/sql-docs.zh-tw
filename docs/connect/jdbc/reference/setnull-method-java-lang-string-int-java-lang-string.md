---
title: setNull 方法 (java.lang.String, int, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setNull (java.lang.String, int, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 16ff77f9-7928-415c-abf6-97ed59e3e396
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b5137c4df92860822e715d70a1355b490026af40
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67973555"
---
# <a name="setnull-method-javalangstring-int-javalangstring"></a>setNull 方法 (java.lang.String, int, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  在給定要設定之參數的類型和名稱時，將指定的參數設定為 null 值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setNull(java.lang.String sCol,  
                    int nType,  
                    java.lang.String sTypeName)  
```  
  
#### <a name="parameters"></a>參數  
 *sCol*  
  
 **String**，包含參數名稱。  
  
 *nType*  
  
 java.sql.Types 所定義的 JDBC 型別程式碼。  
  
 *sTypeName*  
  
 **String**，指出正在設定的參數完整名稱。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setNull 方法由 java.sql.CallableStatement 介面中的 setNull 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [setNull 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setnull-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
