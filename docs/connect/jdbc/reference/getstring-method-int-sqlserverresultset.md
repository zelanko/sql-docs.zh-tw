---
title: "getString 方法 (int) (SQLServerResultSet) |Microsoft 文件"
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
- SQLServerResultSet.getString (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bfa493c4-fe07-449b-b4d0-384e1a1fce48
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2851090b2f22faac3f050ad535ec9f36ac3efae6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getstring-method-int-sqlserverresultset"></a>getString 方法 (int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，這個目前的資料列內指定之資料行索引的[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件當做**字串**在 Java 程式語言。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.String getString(int columnIndex)  
```  
  
#### <a name="parameters"></a>參數  
 *columnIndex*  
  
 **Int** ，指出資料行索引。  
  
## <a name="return-value"></a>傳回值  
 A**字串**值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getString 方法是由 java.sql.ResultSet 介面中的 getString 方法來指定。  
  
 中的所有資料行[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]可以當做字串傳回。 這表示**字串**的所有數字和字元類型，表示和十六進位字串表示法，例如 binary、 varbinary、 varbinary （max）、 映像、 時間戳記，以及 uniqueidentifier、 二進位資料行可以是傳回。  
  
 區分位置的型別 (例如 money、smallmoney、datetime、smalldatetime、float、real、decimal 和 numeric) 將會針對該型別的基礎值傳回標準 toString() 格式。  
  
 使用者定義型別會當做十六進位傳回**字串**值。  
  
## <a name="see-also"></a>另請參閱  
 [getString 方法 &#40;SQLServerResultSet &#41;](../../../connect/jdbc/reference/getstring-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
