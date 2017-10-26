---
title: "setBinaryStream 方法 (SQLServerBlob) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerBlob.setBinaryStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: abcec31f-1a60-4765-9725-8cf7e9f1f8ab
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 630244ef25c3206d9c66ad2797d1a435661d1a60
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="setbinarystream-method-sqlserverblob"></a>setBinaryStream 方法 (SQLServerBlob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取可用來寫入至 BLOB 值的資料流。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.io.OutputStream setBinaryStream(long pos)  
```  
  
#### <a name="parameters"></a>參數  
 *Pos*  
  
 BLOB 值中開始寫入的位置。  
  
## <a name="return-value"></a>傳回值  
 輸出資料流。  
  
## <a name="exceptions"></a>例外狀況  
 java.sql.SQLException  
  
## <a name="remarks"></a>備註  
 這個 setBinaryStream 方法是由 java.sql.Blob 介面中 setBinaryStream 方法指定。  
  
 輸出資料流會從指定的位置開始覆寫 BLOB 中的資料，而且可以超過 BLOB 的初始長度。 指定位置 + 1 的值將會附加位元組。 傳遞位置 + 2 或更大 (或是零或零以下) 的值將會擲回位置錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerBlob 方法](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob 成員](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob 類別](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  

