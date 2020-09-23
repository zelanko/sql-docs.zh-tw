---
description: updateCharacterStream 方法 (int, java.io.Reader, int)
title: updateCharacterStream 方法 (int, java.io.Reader, int)
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateCharacterStream (int, java.io.Reader, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b692c372-f6d7-4528-9c5d-cd8421bdb12e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 29d660a9bc91cc37e3882aa7f9ae025a84c65f4e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458010"
---
# <a name="updatecharacterstream-method-int-javaioreader-int"></a>updateCharacterStream 方法 (int, java.io.Reader, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用字元資料流值來更新指定的資料行，該值將包含指定的字元數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void updateCharacterStream(int columnIndex,  
                                  java.io.Reader readerValue,  
                                  int length)  
```  
  
#### <a name="parameters"></a>參數  
 *columnIndex*  
  
 指出資料行索引的 **int**。  
  
 *readerValue*  
  
 Reader 物件。  
  
 *length* (長度)  
  
 **int**，指出資料流的長度。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 updateCharacterStream 方法是由 java.sql.ResultSet 介面中的 updateCharacterStream 方法所指定。  
  
 這個方法會透過 Reader 物件將 Unicode 字元傳遞到選取的文字和二進位資料行。 這包括所有的文字資料行，以及 **binary**、**varbinary**、**varbinary(max)** 、**image** 和 **xml** 等資料行，但是不包含 **udt** 資料行。  
  
 如果此資料流的長度與 *length* 參數中所指定的長度不同，JDBC 驅動程式就會在更新或插入資料列時擲回例外狀況。  
  
 如果資料流長度為未知，*length* 參數可能會設為 -1，指出驅動程式應接受該資料流 (無論其長度為何)。 針對 sqljdbc4.jar，建議您在應用程式要從長度未知的資料流更新資料行時，使用 JDBC 4.0 方法 [updateCharacterStream 方法 &#40;int, java.io.Reader&#41;](../../../connect/jdbc/reference/updatecharacterstream-method-int-java-io-reader.md)。  
  
## <a name="see-also"></a>另請參閱  
 [updateCharacterStream 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatecharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
