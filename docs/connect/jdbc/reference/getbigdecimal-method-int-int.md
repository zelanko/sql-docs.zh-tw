---
title: getBigDecimal 方法 (int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getBigDecimal (int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d9351b35-7046-4852-a612-72d4c46b2bbb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 77fa7092b7835e400b7ced8c7dbc0368188b0eb8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "67954009"
---
# <a name="getbigdecimal-method-int-int"></a>getBigDecimal 方法 (int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  配合給定的參數索引和小數位數來擷取指定之參數的值當做 java.math.BigDecimal。  
  
> [!NOTE]  
>  這個方法在 JDBC 規格中已被取代。 您應該改用 [getBigDecimal (int)](../../../connect/jdbc/reference/getbigdecimal-method-int.md) 方法。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.math.BigDecimal getBigDecimal(int index,  
                                          int scale)  
```  
  
#### <a name="parameters"></a>參數  
 *index*  
  
 指出參數索引的 **int**。  
  
 *scale*  
  
 **int**，指出小數點右邊的位數。  
  
## <a name="return-value"></a>傳回值  
 BigDecimal 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getBigDecimal 方法是由 java.sql.CallableStatement 介面中的 getBigDecimal 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [getBigDecimal 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getbigdecimal-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
