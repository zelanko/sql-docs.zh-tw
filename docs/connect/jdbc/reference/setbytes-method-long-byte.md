---
title: setBytes 方法 （long，位元組） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerBlob.setBytes (long.byte[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ffb8f107-0f9d-4410-957f-62b718e1e872
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f164a93981bb45d5d3cb5fdba973de4790ca7db5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="setbytes-method-long-byte"></a>setBytes 方法 （long，位元組）
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  從給定位置開始將給定位元組陣列寫入 BLOB，然後傳回寫入的位元組數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int setBytes(long pos,  
                    byte[] bytes)  
```  
  
#### <a name="parameters"></a>參數  
 *pos*  
  
 BLOB 中開始寫入資料的位置 (以 1 為基底)。  
  
 *位元組*  
  
 要寫入 BLOB 中的位元組陣列。  
  
## <a name="return-value"></a>傳回值  
 A**長**值，指定寫入的位元組數目。  
  
## <a name="exceptions"></a>例外狀況  
 java.sql.SQLException  
  
## <a name="remarks"></a>備註  
 這個 setBytes 方法是由 java.sql.Blob 介面中 setBytes 方法指定。  
  
 資料會從指定的位置開始覆寫，而且可以超過 BLOB 的初始長度。 指定位置 + 1 的值將會附加位元組。 傳遞位置 + 2 或更大 (或是零或零以下) 的值將會擲回位置錯誤。 傳遞長度為零**位元組**陣列會傳回零，因為未不寫入任何位元組。  
  
## <a name="see-also"></a>另請參閱  
 [setBytes 方法&#40;SQLServerBlob&#41;](../../../connect/jdbc/reference/setbytes-method-sqlserverblob.md)   
 [SQLServerBlob 方法](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob 成員](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob 類別](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
