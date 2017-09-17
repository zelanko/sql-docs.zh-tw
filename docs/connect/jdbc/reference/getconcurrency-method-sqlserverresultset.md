---
title: "getConcurrency 方法 (SQLServerResultSet) |Microsoft 文件"
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
- SQLServerResultSet.getConcurrency
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 207e25f4-769c-4ff3-913c-3517b06208e4
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: eec9174be2430b8711669e479faea89e34f30b4c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getconcurrency-method-sqlserverresultset"></a>getConcurrency 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取這個並行模式[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getConcurrency()  
```  
  
## <a name="return-value"></a>傳回值  
 **Int**指出並行類型，它可以是下列值之一：  
  
 ResultSet.CONCUR_READ_ONLY  
  
 ResultSet.CONCUR_UPDATABLE  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getConcurrency 方法是由 java.sql.ResultSet 介面中的 getConcurrency 方法指定。  
  
 取決於使用的並行[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)建立結果集的物件。  
  
 這個方法可用來決定實際的並行。 如果應用程式選取 CONCUR_READ_ONLY 或 CONCUR_UPDATABLE，將會傳回這些項目。 如果應用程式使用預設並行，將會傳回 CONCUR_READ_ONLY。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
