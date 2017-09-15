---
title: "getDouble 方法 (int) |Microsoft 文件"
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
- SQLServerCallableStatement.getDouble (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c0ed63bb-5ebe-4155-9f91-8fbfeac9c3b2
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0d2ff23fa5aa85b5d82244647d063a2611240811
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getdouble-method-int"></a>getDouble 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取所指定之參數的值**double**在 Java 程式語言中使用給定的參數索引。  
  
## <a name="syntax"></a>語法  
  
```  
  
public double getDouble(int index)  
```  
  
#### <a name="parameters"></a>參數  
 *索引*  
  
 **Int** ，指出參數索引。  
  
## <a name="return-value"></a>傳回值  
 A **double**值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 GetDouble 方法 java.sql.CallableStatement 介面中所指定此 getDouble 方法。  
  
 這個方法會傳回所有數字資料型別與 Java **double**精確度。  
  
## <a name="see-also"></a>另請參閱  
 [getDouble 方法 &#40;SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getdouble-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
