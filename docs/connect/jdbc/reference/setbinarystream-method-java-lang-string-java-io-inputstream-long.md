---
title: setBinaryStream 方法來輸入資料流-長時間 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d59c7327-c9dc-4e4f-9dff-19e1a3c62eb2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 36ba3cf5fec53024faf83a83d7e9a24116f143be
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47849576"
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
 *parameterName*  
  
 **String**，其中包含參數的名稱。  
  
 *x*  
  
 InputStream 物件。  
  
 *length*  
  
 ，指出位元組數目的長度。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 setBinaryStream 方法 setBinaryStream 方法 java.sql.CallableStatement 介面中所指定。  
  
 如果此資料流的長度與 *length* 參數中所指定的長度不同，JDBC 驅動程式就會在更新或插入資料列時擲回例外狀況。  
  
 如果資料流長度為未知，*length* 參數可能會設為 -1，指出驅動程式應接受該資料流 (無論其長度為何)。 針對 sqljdbc4.jar，建議您在應用程式要從長度未知的資料流更新資料行時，使用 JDBC 4.0 方法 [setBinaryStream 方法 (java.lang.String, java.io.InputStream)](../../../connect/jdbc/reference/setbinarystream-method-java-lang-string-java-io-inputstream.md)。  
  
## <a name="see-also"></a>另請參閱  
 [setBinaryStream &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setbinarystream-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
