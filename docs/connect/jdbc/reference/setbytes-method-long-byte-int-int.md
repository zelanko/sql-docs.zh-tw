---
title: setBytes 方法 (long，byte、 int，int) |Microsoft 文件
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
- SQLServerBlob.setBytes (long.byte[], int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7def226c-b211-459e-8c1a-08592d75d4a4
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4b18005c16cd62358eb5f269504fc9d80eadb6de
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="setbytes-method-long-byte-int-int"></a>setBytes 方法 (long，byte、 int，int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  從給定的位置、位移和長度開始，將給定位元組陣列的全部或一部分寫入 BLOB，然後傳回寫入的位元組數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int setBytes(long pos,  
                    byte[] bytes,  
                    int offset,  
                    int len)  
```  
  
#### <a name="parameters"></a>參數  
 *pos*  
  
 BLOB 中開始寫入資料的位置 (以 1 為基底)。  
  
 *位元組*  
  
 要寫入 BLOB 中的位元組陣列。  
  
 *offset*  
  
 以位元組為單位的位移陣列開始讀取資料來源位置**位元組**陣列。  
  
 *len*  
  
 嘗試從位元組陣列讀到 BLOB 中的位元組數目。  
  
## <a name="return-value"></a>傳回值  
 **Int**包含寫入的位元組數目。  
  
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
  
  
