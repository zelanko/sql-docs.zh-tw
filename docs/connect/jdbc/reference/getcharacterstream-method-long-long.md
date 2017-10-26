---
title: "getCharacterStream 方法 (long，long) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d70f502f-f60f-436a-83e6-797a0ed71bf3
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ba910c36ff82209a668ef6d96987330705703080
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getcharacterstream-method-long-long"></a>getCharacterStream 方法 (long, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回**Clob**資料讀取器物件或字元的指定的位置和長度的資料流。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.io.Reader getCharacterStream(long pos,  
                                         long length)  
```  
  
#### <a name="parameters"></a>參數  
 *pos*  
  
 A**長**，表示要擷取之部分值的第一個字元的位移。  
  
 *length*  
  
 A**長**，表示要擷取之部分值的字元長度。  
  
## <a name="return-value"></a>傳回值  
 讀取器物件，其中包含**Clob**資料。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getCharacterStream 方法是由 java.sql.Clob 介面中的 getCharacterStream 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [getCharacterStream 方法 &#40;SQLServerClob &#41;](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverclob.md)   
 [SQLServerClob 方法](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob 成員](../../../connect/jdbc/reference/sqlserverclob-members.md)  
  
  

