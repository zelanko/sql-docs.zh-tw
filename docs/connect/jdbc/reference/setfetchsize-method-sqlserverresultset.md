---
title: "setFetchSize 方法 (SQLServerResultSet) |Microsoft 文件"
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
- SQLServerResultSet.setFetchSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 233bf4f8-4758-42d0-a80b-33e34fa78027
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ed3f37d12253c03ae192b03db27caf4d180e568d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="setfetchsize-method-sqlserverresultset"></a>setFetchSize 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  提供 JDBC 驅動程式提示，當做這個需要更多的資料列時應該從資料庫提取的資料列數目[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setFetchSize(int rows)  
```  
  
#### <a name="parameters"></a>參數  
 *資料列*  
  
 **Int**指出要提取的資料列數目。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 setFetchSize 方法是由 java.sql.ResultSet 介面中的 setFetchSize 方法指定。  
  
 如果指定的提取大小為零，則 JDBC 驅動程式會忽略此值，並預估應有的提取大小。 預設值由設定[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)建立結果集的物件。 提取大小可以隨時變更。  
  
 這個方法會變更伺服器資料指標的區塊提取大小，並在下一次 JDBC 驅動程式需要呼叫 sp_cursorfetch 時生效。 將提取大小設定為零會還原目前使用中之資料指標類型的預設提取大小。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

