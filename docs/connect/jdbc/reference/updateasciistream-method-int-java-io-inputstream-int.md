---
title: updateAsciiStream 方法 (java.io.InputStream, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateAsciiStream (int, java.io.InputStream.int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d07944b8-7001-49b5-b3b3-0676f71e17cf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 843cb16fab8b05ae72c502fecd171f9af2886779
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "68213652"
---
# <a name="updateasciistream-method-int-javaioinputstream-int"></a>updateAsciiStream 方法 (int, java.io.InputStream, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用 ASCII 資料流值來更新指定的資料行，該值將包含指定的位元組數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void updateAsciiStream(int index,  
                              java.io.InputStream x,  
                              int length)  
```  
  
#### <a name="parameters"></a>參數  
 *index*  
  
 指出資料行索引的 **int**。  
  
 *x*  
  
 InputStream 物件。  
  
 *length*  
  
 **int**，指出資料流的長度。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 updateAsciiStream 方法是由 java.sql.ResultSet 介面中的 updateAsciiStream 方法指定。  
  
 這個方法會從 InputStream 物件，將 ASCII 字元 (位元組) 傳遞到可轉換的字元資料行，這些是 Unicode 的 ASCII 範圍 [0x00 - 0x7F]，以及 874、932、936、949、950 和 1250 到 1258 的字碼頁。 這個方法會執行轉換，直到目的地定序頁面。 嘗試更新無法轉換的目的地資料行，將擲回例外狀況。 若是處理二進位資料行，則會傳遞未經處理位元組。  
  
 如果此資料流的長度與 *length* 參數中所指定的長度不同，JDBC 驅動程式就會在更新或插入資料列時擲回例外狀況。  
  
 如果資料流長度為未知，*length* 參數可能會設為 -1，指出驅動程式應接受該資料流 (無論其長度為何)。 針對 sqljdbc4.jar，建議您在應用程式要從長度未知的資料流更新資料行時，使用 JDBC 4.0 方法 [updateAsciiStream 方法 &#40;int, java.io.InputStream&#41;](../../../connect/jdbc/reference/updateasciistream-method-int-java-io-inputstream.md)。  
  
## <a name="see-also"></a>另請參閱  
 [updateAsciiStream 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
