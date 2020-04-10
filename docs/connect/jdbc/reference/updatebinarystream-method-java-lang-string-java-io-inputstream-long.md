---
title: updateBinaryStream 方法 (java.io.InputStream, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d3c0fb5d-ca05-43f7-9f38-fba6cf3705c6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0098e80556a129aad720b133f7eeca1ebfc22b6e
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924982"
---
# <a name="updatebinarystream-method-javalangstring-javaioinputstream-long"></a>updateBinaryStream 方法 (java.lang.String, java.io.InputStream, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用二進位資料流值來更新指定的資料行，該值將包含指定的位元組數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void updateBinaryStream(java.lang.String columnLabel,  
                               java.io.InputStream x,  
                               long length)  
```  
  
#### <a name="parameters"></a>參數  
 *columnLabel*  
  
 String，包含資料行標籤。  
  
 *x*  
  
 InputStream 物件。  
  
 *length*  
  
 **long**，指出資料流的長度。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 updateBinaryStream 方法是由 java.sql.ResultSet 介面中的 updateBinaryStream 方法指定。  
  
 這個方法會透過 InputStream 物件將位元組傳遞到選取的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 二進位資料行，例如 binary、varbinary、varbinary(max)、image、xml 和 udt。 這個方法不支援更新字元資料行。 若要以 InputStream 更新字元資料行，請使用 [updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md) 方法。  
  
 如果此資料流的長度與 *length* 參數中所指定的長度不同，JDBC 驅動程式就會在更新或插入資料列時擲回例外狀況。  
  
 如果資料流長度為未知，*length* 參數可能會設為 -1，指出驅動程式應接受該資料流 (無論其長度為何)。 針對 sqljdbc4.jar，建議您在應用程式要從長度未知的資料流更新資料行時，使用 JDBC 4.0 方法 [setBinaryStream 方法 &#40;java.lang.String, java.io.InputStream&#41;](../../../connect/jdbc/reference/updatebinarystream-method-java-lang-string-java-io-inputstream.md)。  
  
## <a name="see-also"></a>另請參閱  
 [updateBinaryStream 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
