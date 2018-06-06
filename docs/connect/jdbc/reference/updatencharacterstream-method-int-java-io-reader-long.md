---
title: updateNCharacterStream 方法 （int，java.io.Reader，long） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: aeec0a56-038e-45b1-98c8-b1046ebd25db
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d6a8956a4722a9fe35e78b6b730da0c88be6e4c0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="updatencharacterstream-method-int-javaioreader-long"></a>updateNCharacterStream 方法 (int, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用字元資料流值來更新指定的資料行，該值將包含指定的位元組數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void updateNCharacterStream(int columnIndex,  
                                    java.io.Reader x,  
                                    long length)  
```  
  
#### <a name="parameters"></a>參數  
 *columnIndex*  
  
 指出資料行索引的 **int**。  
  
 *x*  
  
 讀取器物件。  
  
 *長度*  
  
 資料流的長度。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 UpdateNCharacterStream 方法 java.sql.ResultSet 介面中所指定此 updateNCharacterStream 方法。  
  
 這個方法會將 Unicode 字元傳遞從讀取器物件選取**nchar**， **nvarchar （max)**， **ntext**，和**xml**資料行。 在其他資料類型資料行上使用這個方法，將會擲回例外狀況。  
  
 如果資料流的長度就是不同於以指定的內容*長度*參數，JDBC 驅動程式會擲回例外狀況時更新或插入資料列。  
  
 如果資料流長度未知，*長度*參數可能會設定為-1，指出驅動程式應該接受資料流，無論其長度為何。 針對 sqljdbc4.jar，我們建議您使用 JDBC 4.0 方法[updateNCharacterStream 方法&#40;int，java.io.Reader&#41; ](../../../connect/jdbc/reference/updatencharacterstream-method-int-java-io-reader.md)應用程式要從長度未知的資料流的資料行的更新。  
  
## <a name="see-also"></a>另請參閱  
 [updateNCharacterStream 方法&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
