---
title: "getByte 方法 (java.lang.String) (SQLServerResultSet) |Microsoft 文件"
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
- SQLServerResultSet.getByte (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 069c68ff-442d-4104-917f-3445a3ad264a
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e3ba04222dd0f578554e42aaa452a32de5ab76a7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getbyte-method-javalangstring-sqlserverresultset"></a>getByte 方法 (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，這個目前的資料列內指定之資料行名稱的[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件當做**位元組**在 Java 程式語言。  
  
## <a name="syntax"></a>語法  
  
```  
  
public byte getByte(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>參數  
 *columnName*  
  
 A**字串**，其中包含資料行名稱。  
  
## <a name="return-value"></a>傳回值  
 A**位元組**值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 GetByte 方法 java.sql.ResultSet 介面中所指定此 getByte 方法。  
  
 這個方法僅支援[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]可以安全傳回位元組值，如 tinyint 和 bit 資料類型。 所有其他資料類型將會擲回例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [getByte 方法 &#40;SQLServerResultSet &#41;](../../../connect/jdbc/reference/getbyte-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
