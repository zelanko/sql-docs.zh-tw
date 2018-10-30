---
title: updateNCharacterStream 方法 (int, java.io.Reader, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: aeec0a56-038e-45b1-98c8-b1046ebd25db
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5fad76cca594595a5efbf16a334975869684a039
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47624866"
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
  
 *length*  
  
 資料流的長度。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 UpdateNCharacterStream 方法 java.sql.ResultSet 介面中所指定這個 updateNCharacterStream 方法。  
  
 這個方法會傳遞到選取的讀取器物件的 Unicode 字元**nchar**， **nvarchar （max)**， **ntext**，以及**xml**資料行。 在其他資料類型資料行上使用這個方法，將會擲回例外狀況。  
  
 如果此資料流的長度與 *length* 參數中所指定的長度不同，JDBC 驅動程式就會在更新或插入資料列時擲回例外狀況。  
  
 如果資料流長度為未知，*length* 參數可能會設為 -1，指出驅動程式應接受該資料流 (無論其長度為何)。 針對 sqljdbc4.jar，建議您在應用程式要從長度未知的資料流更新資料行時，使用 JDBC 4.0 方法 [updateNCharacterStream 方法 &#40;int, java.io.Reader&#41;](../../../connect/jdbc/reference/updatencharacterstream-method-int-java-io-reader.md)。  
  
## <a name="see-also"></a>另請參閱  
 [updateNCharacterStream 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
