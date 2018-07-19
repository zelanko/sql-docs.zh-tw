---
title: setCharacterStream 方法 （int，java.io.Reader，int） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setCharacterStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 139a5b74-8d7d-41cf-991a-a142349c58f6
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 06d5f6721efb91f3e92a9ba778bb4b43d8b08da4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32843163"
---
# <a name="setcharacterstream-method-int-javaioreader-int"></a>setCharacterStream 方法 (int, java.io.Reader, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定的參數設定為給定的讀取器物件，這是給定的字元數。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setCharacterStream(int n,  
                                     java.io.Reader reader,  
                                     int length)  
```  
  
#### <a name="parameters"></a>參數  
 *n*  
  
 **Int** ，指出參數編號。  
  
 *reader*  
  
 讀取器物件。  
  
 *長度*  
  
 字元數。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 setCharacterStream 方法 setCharacterStream 方法 java.sql.PreparedStatement 介面中所指定。  
  
 如果資料流的長度不同中指定*長度*參數，JDBC 驅動程式會擲回例外狀況時更新或插入資料列。  
  
 如果資料流長度未知，*長度*參數可能會設定為-1，指出驅動程式應該接受資料流，無論其長度為何。 針對 sqljdbc4.jar，我們建議您使用 JDBC 4.0 方法[setCharacterStream 方法&#40;int，java.io.Reader&#41; ](../../../connect/jdbc/reference/setcharacterstream-method-int-java-io-reader.md)應用程式要從長度未知的資料流的資料行的更新。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerPreparedStatement 成員](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 類別](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
