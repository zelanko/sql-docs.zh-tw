---
title: "getNClob 方法 (java.lang.String) (SQLServerResultSet) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 36571f7c-b335-4249-8f83-51dcb6923aec
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8ef00d0c7a72e891364fad57e0fa0d35a3814799
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getnclob-method-javalangstring-sqlserverresultset"></a>getNClob 方法 (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取目前資料列內指定的資料行的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)當做 NClob 物件在 Java 程式語言中的物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.NClob getNClob(java.lang.String columnLabel)  
```  
  
#### <a name="parameters"></a>參數  
 *columnLable*  
  
 A**字串**，其中包含資料行標籤。  
  
## <a name="return-value"></a>傳回值  
 NClob 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 GetNClob 方法 java.sql.ResultSet 介面中所指定此 getNClob 方法。  
  
 這個方法僅支援**nvarchar （max)**， **ntext**，和**xml**資料行。 對任何其他資料類型使用這個方法，將擲回例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [getNClob 方法 &#40;SQLServerResultSet &#41;](../../../connect/jdbc/reference/getnclob-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
