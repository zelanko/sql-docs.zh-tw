---
title: getMaxFieldSize 方法 (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getMaxFieldSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ed7bbcb8-660b-4e9b-8241-e216c42826f9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9a1700cc8bb2bfb54dd9ddee52da54899f764650
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67982099"
---
# <a name="getmaxfieldsize-method-sqlserverstatement"></a>getMaxFieldSize 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取最大位元組數目，此位元組可傳回作為 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中字元和二進位資料行的值．而該物件是由這個 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 物件產生。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final int getMaxFieldSize()  
```  
  
## <a name="return-value"></a>傳回值  
 **int**，指出資料行可以包含的最大位元組數目，如果沒有任何限制，則為 0。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getMaxFieldSize 方法是由 java.sql.Statement 介面中的 getMaxFieldSize 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerStatement 方法](../../../connect/jdbc/reference/sqlserverstatement-methods.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
