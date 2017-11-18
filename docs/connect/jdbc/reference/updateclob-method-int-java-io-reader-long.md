---
title: "updateClob 方法 （int，java.io.Reader，long） |Microsoft 文件"
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
ms.assetid: 5c958ccb-386a-4dd5-901d-5a106dac2683
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fa84650a36e24959564d304f1c6da947b9b5cb1e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="updateclob-method-int-javaioreader-long"></a>updateClob 方法 (int, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用指定的 Reader 物件更新指定的資料行，該物件長度為指定的字元數。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void updateClob(int columnIndex,  
                        java.io.Reader reader,  
                        long length)  
```  
  
#### <a name="parameters"></a>參數  
 *columnIndex*  
  
 **Int** ，指出資料行索引。  
  
 *讀取器*  
  
 讀取器物件。  
  
 *length*  
  
 參數資料中的字元數目。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 UpdateClob 方法 java.sql.ResultSet 介面中所指定此 updateClob 方法。  
  
## <a name="see-also"></a>另請參閱  
 [updateClob 方法 &#40;SQLServerResultSet &#41;](../../../connect/jdbc/reference/updateclob-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

