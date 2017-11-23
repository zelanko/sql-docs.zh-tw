---
title: "setBinaryStream 方法來輸入資料流的長度 |Microsoft 文件"
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
ms.assetid: d59c7327-c9dc-4e4f-9dff-19e1a3c62eb2
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5e2bafcd7f42f7bee633f3969e9222ddcba8a0df
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="setbinarystream-method-javalangstring-javaioinputstream-long"></a>setBinaryStream 方法 (java.lang.String, java.io.InputStream, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將指定的參數設定為指定的輸入資料流，其中將包含指定的位元組數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setBinaryStream(java.lang.String parameterName,  
                            java.io.InputStream x,  
                            long length)  
```  
  
#### <a name="parameters"></a>參數  
 *參數名稱*  
  
 A**字串**，其中包含參數的名稱。  
  
 *x*  
  
 InputStream 物件。  
  
 *length*  
  
 A**長**，指出位元組數目的長度。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 setBinaryStream 方法 setBinaryStream 方法 java.sql.CallableStatement 介面中所指定。  
  
 如果資料流的長度就是不同於以指定的內容*長度*參數，JDBC 驅動程式會擲回例外狀況時更新或插入資料列。  
  
 如果資料流長度未知，*長度*參數可能會設定為-1，指出驅動程式應該接受資料流，無論其長度為何。 針對 sqljdbc4.jar，我們建議您使用 JDBC 4.0 方法[setBinaryStream 方法 （java.lang.String，java.io.InputStream）](../../../connect/jdbc/reference/setbinarystream-method-java-lang-string-java-io-inputstream.md)應用程式要從長度未知的資料流的資料行的更新。  
  
## <a name="see-also"></a>請參閱＜  
 [setBinaryStream &#40;SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/setbinarystream-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
