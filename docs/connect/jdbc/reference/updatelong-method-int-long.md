---
title: updateLong 方法 (int, long) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateLong (int, long)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f6363288-1415-4b25-8bb3-c34d6211c6d7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8e8d0ad2332d1990445b8c6fb3c1ebd5914453d4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67998803"
---
# <a name="updatelong-method-int-long"></a>updateLong 方法 (int, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  透過指定的資料行索引，使用 **long** 值來更新指定的資料行。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void updateLong(int index,  
                       long x)  
```  
  
#### <a name="parameters"></a>參數  
 *index*  
  
 指出資料行索引的 **int**。  
  
 *x*  
  
 **Long**值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 updateLong 方法是由 java.sql.ResultSet 介面中的 updateLong 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [updateLong 方法&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatelong-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
