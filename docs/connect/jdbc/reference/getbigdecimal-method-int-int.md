---
title: getBigDecimal 方法 （int，int） |Microsoft 文件
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
- SQLServerCallableStatement.getBigDecimal (int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d9351b35-7046-4852-a612-72d4c46b2bbb
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2f52732b2e6b752713dc62c377e7038d61c4d3b3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32833773"
---
# <a name="getbigdecimal-method-int-int"></a>getBigDecimal 方法 (int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  配合給定的參數索引和小數位數來擷取指定之參數的值當做 java.math.BigDecimal。  
  
> [!NOTE]  
>  這個方法在 JDBC 規格中已被取代。 相反地，您應該使用[getBigDecimal (int)](../../../connect/jdbc/reference/getbigdecimal-method-int.md)方法。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.math.BigDecimal getBigDecimal(int index,  
                                          int scale)  
```  
  
#### <a name="parameters"></a>參數  
 *索引*  
  
 指出參數索引的 **int**。  
  
 *scale*  
  
 **Int** ，指出小數點右邊的位數。  
  
## <a name="return-value"></a>傳回值  
 BigDecimal 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 GetBigDecimal 方法 java.sql.CallableStatement 介面中所指定這個 getBigDecimal 方法。  
  
## <a name="see-also"></a>另請參閱  
 [getBigDecimal 方法&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getbigdecimal-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
