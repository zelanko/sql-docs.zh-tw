---
title: setBytes 方法 (long, byte, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerBlob.setBytes (long.byte[], int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7def226c-b211-459e-8c1a-08592d75d4a4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eaa3f23fdf9b38553b3492ca96895645dc8de371
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80929142"
---
# <a name="setbytes-method-long-byte-int-int"></a>setBytes 方法 (long, byte, int, int)
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
  
 *bytes*  
  
 要寫入 BLOB 中的位元組陣列。  
  
 *offset*  
  
 位元組陣列中開始從 **byte** 陣列讀取資料的位移。  
  
 *len*  
  
 嘗試從位元組陣列讀到 BLOB 中的位元組數目。  
  
## <a name="return-value"></a>傳回值  
 **int**，其中包含寫入的位元組數目。  
  
## <a name="exceptions"></a>例外狀況  
 java.sql.SQLException  
  
## <a name="remarks"></a>備註  
 這個 setBytes 方法是由 java.sql.Blob 介面中的 setBytes 方法指定。  
  
 資料會從指定的位置開始覆寫，而且可以超過 BLOB 的初始長度。 指定位置 + 1 的值將會附加位元組。 傳遞位置 + 2 或更大 (或是零或零以下) 的值將會擲回位置錯誤。 傳遞長度為零的 **byte** 陣列將會傳回零，因為未寫入任何位元組。  
  
## <a name="see-also"></a>另請參閱  
 [setBytes 方法 &#40;SQLServerBlob&#41;](../../../connect/jdbc/reference/setbytes-method-sqlserverblob.md)   
 [SQLServerBlob 方法](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob 成員](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob 類別](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
