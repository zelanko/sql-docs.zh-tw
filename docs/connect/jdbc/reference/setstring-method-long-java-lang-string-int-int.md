---
title: setString 方法 (long, java.lang.String, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.setString (long, java.lang.String, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9fb59b09-e825-46a6-ba5d-85d4a8dc143a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ad0f8e51b0663c771c1ee519ac318a13264aa7e5
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80917054"
---
# <a name="setstring-method-long-javalangstring-int-int"></a>setString 方法 (long, java.lang.String, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  依據給定的位移和長度，在給定位置開始將給定字串寫入 CLOB。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int setString(long pos,  
                     java.lang.String str,  
                     int offset,  
                     int len)  
```  
  
#### <a name="parameters"></a>參數  
 *pos*  
  
 開始寫入 CLOB 的位置。  
  
 *str*  
  
 要寫入 CLOB 的字串。  
  
 *offset*  
  
 字串內要開始讀取字元的位移。  
  
 *len*  
  
 要寫入的字元數。  
  
## <a name="return-value"></a>傳回值  
 寫入的字元數。  
  
## <a name="exceptions"></a>例外狀況  
 java.sql.SQLException  
  
## <a name="remarks"></a>備註  
 這個 setString 方法是由 java.sql.Clob 介面中的 setString 方法指定。  
  
 字元資料會從指定的位置開始覆寫，而且可以覆寫 CLOB 的初始長度。 指定位置 + 1 的值將會附加字串。 指定位置 + 2 或更大 (或是零或零以下) 的值將會擲回位置錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [setString 方法 &#40;SQLServerClob&#41;](../../../connect/jdbc/reference/setstring-method-sqlserverclob.md)   
 [SQLServerClob 方法](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob 成員](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob 類別](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
