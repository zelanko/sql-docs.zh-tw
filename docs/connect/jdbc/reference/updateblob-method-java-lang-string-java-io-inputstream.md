---
title: updateBlob 方法 （java.lang.String，java.io.InputStream） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 018cd71b-4b58-49a7-990e-d28dbb12da70
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3253fd541aa4b86034d96897d182f76b0d10ceeb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="updateblob-method-javalangstring-javaioinputstream"></a>updateBlob 方法 (java.lang.String, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用指定的輸入資料流，更新指定的資料行。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void updateBlob(java.lang.String columnLabel,  
                       java.io.InputStream inputStream)  
```  
  
#### <a name="parameters"></a>參數  
 *columnLabel*  
  
 A**字串**，其中包含資料行標籤。  
  
 *inputStream*  
  
 InputStream 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 UpdateBlob 方法 java.sql.ResultSet 介面中所指定此 updateBlob 方法。  
  
## <a name="see-also"></a>另請參閱  
 [updateBlob 方法&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateblob-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
