---
title: setAsciiStream 方法 (int, java.io.InputStream, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9dfa7781-d72f-407a-a8d4-1c78c9446d09
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 269392af66afc7ddc3aadc2f2f10e67a5b422859
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47610276"
---
# <a name="setasciistream-method-int-javaioinputstream-long"></a>setAsciiStream 方法 (int, java.io.InputStream, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將指定的參數號碼設定為所指定 java.io.InputStream 物件，該物件具有指定的位元組數。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setAsciiStream(int parameterIndex,  
                                 java.io.InputStream x,  
                                    long length)  
```  
  
#### <a name="parameters"></a>參數  
 *parameterIndex*  
  
 **int**，指出參數編號。  
  
 *x*  
  
 Java.io.InputStream 物件。  
  
 *length*  
  
 **long**，指定位元組的數目。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 setAsciiStream 方法是由 java.sql.PreparedStatement 介面中的 setAsciiStream 方法指定。  
  
 如果此資料流的長度與 *length* 參數中所指定的長度不同，JDBC 驅動程式就會在更新或插入資料列時擲回例外狀況。  
  
 如果資料流長度為未知，*length* 參數可能會設為 -1，指出驅動程式應接受該資料流 (無論其長度為何)。 針對 sqljdbc4.jar，建議您在應用程式要從長度未知的資料流更新資料行時，使用 JDBC 4.0 方法 [setAsciiStream 方法 &#40;int, java.io.InputStream&#41;](../../../connect/jdbc/reference/setasciistream-method-int-java-io-inputstream.md)。  
  
## <a name="see-also"></a>另請參閱  
 [setAsciiStream 方法 &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setasciistream-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 成員](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
