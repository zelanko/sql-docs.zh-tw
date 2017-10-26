---
title: "getBlob 方法 (java.lang.String) |Microsoft 文件"
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
- SQLServerCallableStatement.getBlob (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3fe74b50-9ccd-4973-a93a-6da2c20a4154
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 920664ef12bbd45f312c32ce69b35cd568531240
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getblob-method-javalangstring"></a>getBlob 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  當做 Blob 物件中給定的參數名稱使用 Java 程式語言，擷取指定之 JDBC BLOB 參數的值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Blob getBlob(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>參數  
 *sCol*  
  
 A**字串**，其中包含參數名稱。  
  
## <a name="return-value"></a>傳回值  
 Blob 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 GetBlob 方法 java.sql.CallableStatement 介面中所指定此 getBlob 方法。  
  
## <a name="see-also"></a>另請參閱  
 [getBlob 方法 &#40;SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getblob-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

