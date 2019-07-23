---
title: prepareStatement 方法 (java.lang.String, int, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.prepareStatement (java.lang.String, int, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b78d2192-f315-4c45-9051-c77059e2c3f4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4a47ac1202ec73c15198b9b6f3c87ee53e027c83
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67976178"
---
# <a name="preparestatement-method-javalangstring-int-int-int"></a>prepareStatement 方法 (java.lang.String, int, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  建立 [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 物件，它會產生具有指定類型、並行和保留性的 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.PreparedStatement prepareStatement(java.lang.String sql,  
                                                   int nType,  
                                                   int nConcur,  
                                                   int nHold)  
```  
  
#### <a name="parameters"></a>參數  
 *sql*  
  
 **String**，其中包含 SQL 陳述式。  
  
 *nType*  
  
 **int**，指出結果集類型。  
  
 *nConcur*  
  
 **int**，指出結果集的並行類型。  
  
 *nHold*  
  
 **int**，指出結果集的保留性。  
  
## <a name="return-value"></a>傳回值  
 JAVA.sql.preparedstatement 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 prepareStatement 方法是由連接介面中的 prepareStatement 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [prepareStatement 方法 &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md)   
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
