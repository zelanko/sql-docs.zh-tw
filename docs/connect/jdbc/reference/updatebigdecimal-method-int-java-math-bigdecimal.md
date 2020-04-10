---
title: updateBigDecimal 方法 (int, java.math.BigDecimal) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateBigDecimal (int, java.math.BigDecimal)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1e15de27-a490-45cd-a3a6-a49721f15a97
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7f3b05d564b857f5e9d096e4ad3fec7593965986
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922892"
---
# <a name="updatebigdecimal-method-int-javamathbigdecimal"></a>updateBigDecimal 方法 (int, java.math.BigDecimal)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  透過指定的資料行索引，使用 BigDecimal 物件來更新指定的資料行。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void updateBigDecimal(int index,  
                             java.math.BigDecimal x)  
```  
  
#### <a name="parameters"></a>參數  
 *index*  
  
 指出資料行索引的 **int**。  
  
 *x*  
  
 BigDecimal 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 updateBigDecimal 方法是由 java.sql.ResultSet 介面中的 updateBigDecimal 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [updateBigDecimal 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatebigdecimal-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
