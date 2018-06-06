---
title: updateClob 方法 （int，java.io.Reader，long） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5c958ccb-386a-4dd5-901d-5a106dac2683
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 978c5f09f2c7524462dc950a5edc9b435324bdb5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
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
  
 指出資料行索引的 **int**。  
  
 *reader*  
  
 讀取器物件。  
  
 *長度*  
  
 參數資料中的字元數目。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 UpdateClob 方法 java.sql.ResultSet 介面中所指定此 updateClob 方法。  
  
## <a name="see-also"></a>另請參閱  
 [updateClob 方法&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateclob-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
