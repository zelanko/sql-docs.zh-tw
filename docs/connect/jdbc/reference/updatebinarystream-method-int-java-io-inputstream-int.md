---
title: "updateBinaryStream 方法 （int，java.io.InputStream，int） |Microsoft 文件"
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
apiname:
- SQLServerResultSet.updateBinaryStream (int, java.io.InputStream, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c8e55377-aaea-4415-8159-938fab1b2a93
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 28786410a4f473ffae34b1036b099e37f81cb885
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="updatebinarystream-method-int-javaioinputstream-int"></a>updateBinaryStream 方法 (int, java.io.InputStream, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用二進位資料流值來更新指定的資料行，該值將包含指定的位元組數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void updateBinaryStream(int columnIndex,  
                               java.io.InputStream x,  
                               int length)  
```  
  
#### <a name="parameters"></a>參數  
 *columnIndex*  
  
 **Int** ，指出資料行索引。  
  
 *x*  
  
 InputStream 物件。  
  
 *length*  
  
 **Int** ，指出資料流的長度。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 UpdateBinaryStream 方法 java.sql.ResultSet 介面中所指定此 updateBinaryStream 方法。  
  
 這個方法會將位元組傳遞從 InputStream 物件選取[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]例如 binary、 varbinary、 varbinary （max）、 影像、 xml 和 udt 的二進位資料行。 這個方法不支援更新字元資料行。 若要更新 InputStream 字元資料行，請使用[updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md)方法。  
  
 如果資料流的長度不同中指定*長度*參數，JDBC 驅動程式會擲回例外狀況時更新或插入資料列。  
  
 如果資料流長度未知，*長度*參數可能會設定為-1，指出驅動程式應該接受資料流，無論其長度為何。 針對 sqljdbc4.jar，我們建議您使用 JDBC 4.0 方法[updateBinaryStream 方法 &#40; int，java.io.InputStream &#41;](../../../connect/jdbc/reference/updatebinarystream-method-int-java-io-inputstream.md)應用程式要從長度未知的資料流的資料行的更新。  
  
## <a name="see-also"></a>另請參閱  
 [updateBinaryStream 方法 &#40;SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

