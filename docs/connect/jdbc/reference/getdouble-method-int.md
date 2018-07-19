---
title: getDouble 方法 (int) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getDouble (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c0ed63bb-5ebe-4155-9f91-8fbfeac9c3b2
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b3b9c1d39e99e40236874a61e3a667985a3a645e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32834253"
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
  
 指出參數索引的 **int**。  
  
## <a name="return-value"></a>傳回值  
 A **double**值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 GetDouble 方法 java.sql.CallableStatement 介面中所指定此 getDouble 方法。  
  
 這個方法會傳回所有數字資料型別與 Java **double**精確度。  
  
## <a name="see-also"></a>另請參閱  
 [getDouble 方法&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getdouble-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
