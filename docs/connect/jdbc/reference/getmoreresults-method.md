---
title: "getMoreResults 方法 （) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerStatement.getMoreResults ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: df89db50-0b2f-4094-820a-30be25ad72fe
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8259b562590d21c57f0780260f50bf15032a7ead
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getmoreresults-method-"></a>getMoreResults 方法 ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  移至下一步的結果[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final boolean getMoreResults()  
```  
  
## <a name="return-value"></a>傳回值  
 **true**如果傳回的結果是結果集。 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 GetMoreResults 方法 java.sql.Statement 介面中所指定此 getMoreResults 方法。  
  
 隱含地呼叫 getMoreResults 方法會關閉與取得的任何目前開啟的結果集物件[getResultSet](../../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md)方法。  
  
## <a name="see-also"></a>另請參閱  
 [getMoreResults 方法 &#40;SQLServerStatement &#41;](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)   
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
