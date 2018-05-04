---
title: getBinaryStream 方法 (int) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerResultSet.getBinaryStream (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: de22a6c4-1ba3-4ed0-91a2-bf235c2ceec3
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fe75fd75dd6695da0651b4f6eb9e9a2292a0807e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="getbinarystream-method-int"></a>getBinaryStream 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，這個目前的資料列內指定之資料行索引的[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)當做不中斷位元組的二進位資料流的物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.io.InputStream getBinaryStream(int columnIndex)  
```  
  
#### <a name="parameters"></a>參數  
 *columnIndex*  
  
 **Int** ，指出資料行索引。  
  
## <a name="return-value"></a>傳回值  
 InputStream 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 GetBinaryStream 方法 java.sql.ResultSet 介面中所指定此 getBinaryStream 方法。  
  
 這個方法可以只用於[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]binary、 varbinary、 varbinary （max） 和 image 資料型別。 嘗試搭配其他資料型別使用這個方法將會擲回例外狀況。  
  
 當這個方法以資料流形式取得值之後，該值可以在資料流的區塊中讀取。 這個方法特別適合用來擷取大型的 LONGVARBINARY 值。  
  
> [!NOTE]  
>  必須先讀取傳回之資料流中的所有資料，然後才可以取得其他任何資料行的值。 下一次呼叫 getter 方法時會以隱含方式關閉此資料流。 此外，資料流可以傳回 0 InputStream.available 方法呼叫時，是否有資料可用。  
  
## <a name="see-also"></a>另請參閱  
 [getBinaryStream 方法&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getbinarystream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
