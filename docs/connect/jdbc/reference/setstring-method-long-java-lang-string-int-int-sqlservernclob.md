---
title: "setString 方法 (long，java.lang.String，int，int)-NClob |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2d5e9f50-15b2-4c76-8bfc-3b5be49c2781
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d09ee2a09d313a192d30dc09ff07f4f3bd35d499
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="setstring-method-long-javalangstring-int-int-sqlservernclob"></a>setString 方法 (long, java.lang.String, int, int) (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定位置開始，依據指定的位移和長度 NCLOB 中寫入指定的字串。  
  
## <a name="syntax"></a>語法  
  
```  
  
int setString(long pos,  
              java.lang.String str,  
              int offset,  
              int len)  
```  
  
#### <a name="parameters"></a>參數  
 *pos*  
  
 要開始寫入位置**NCLOB**; 第一個位置是 1。  
  
 *str*  
  
 要寫入的字串**NCLOB**。  
  
 *位移*  
  
 中的位移*str*来開始讀取要寫入的字元。  
  
 *len*  
  
 要寫入的字元數。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 SetString 方法 java.sql.NClob 介面中所指定此 setString 方法。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerNClob 方法](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [SQLServerNClob 成員](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [SQLServerNClob 類別](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  

