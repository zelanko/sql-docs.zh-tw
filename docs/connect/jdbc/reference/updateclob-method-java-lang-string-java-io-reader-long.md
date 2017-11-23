---
title: "updateClob 方法 （java.lang.String，java.io.Reader，long） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6b8f759a-ce5d-41b2-b6cc-24a3ab299f1f
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1e839bbdd8bb4fa4641075ce5cbaf82aef198326
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="updateclob-method-javalangstring-javaioreader-long"></a>updateClob 方法 (java.lang.String, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用指定的 Reader 物件更新指定的資料行，該物件長度為指定的字元數。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void updateClob(java.lang.String columnLabel,  
                        java.io.Reader reader,  
                        long length)  
```  
  
#### <a name="parameters"></a>參數  
 *columnLabel*  
  
 A**字串**，其中包含資料行標籤。  
  
 *讀取器*  
  
 讀取器物件。  
  
 *length*  
  
 參數資料中的字元數目。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 UpdateClob 方法 java.sql.ResultSet 介面中所指定此 updateClob 方法。  
  
## <a name="see-also"></a>請參閱＜  
 [updateClob 方法 &#40;SQLServerResultSet &#41;](../../../connect/jdbc/reference/updateclob-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
