---
title: "getNCharacterStream 方法 (java.lang.String) (SQLServerResultSet) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a117f3a3-9c25-41e1-9adb-a40e90620dd6
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f846c2c2a008fae97bfb61dbd2495ae33b05f3f2
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getncharacterstream-method-javalangstring-sqlserverresultset"></a>getNCharacterStream 方法 (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取目前資料列內指定的資料行的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件做為讀取器物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.io.Reader getNCharacterStream(java.lang.String columnLabel)  
```  
  
#### <a name="parameters"></a>參數  
 *columnLabel*  
  
 字串，包含資料行標籤。  
  
## <a name="return-value"></a>傳回值  
 讀取器物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 GetNCharacterStream 方法 java.sql.ResultSet 介面中所指定此 getNCharacterStream 方法。  
  
 這個方法可以用來擷取值的**nvarchar**， **nchar**， **nvarchar （max)**， **ntext**，或**xml**中目前資料列，這個資料行[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。 如果嘗試使用這個方法來擷取其他資料類型的值，將擲回例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [getNCharacterStream 方法 &#40;SQLServerResultSet &#41;](../../../connect/jdbc/reference/getncharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)  
  
  
