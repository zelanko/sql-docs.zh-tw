---
title: setString 方法 (long，java.lang.String) |Microsoft 文件
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
- SQLServerClob.setString (long, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1b2190e9-5ace-497a-8554-0e913ea9b0cb
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7194a8778ecae136d7a70086c5fa2e9353988a93
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="setstring-method-long-javalangstring"></a>setString 方法 (long, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  寫入指定**字串**clob 從給定位置開始。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int setString(long pos,  
                     java.lang.String s)  
```  
  
#### <a name="parameters"></a>參數  
 *pos*  
  
 開始寫入 CLOB 的位置。  
  
 *S*  
  
 **字串**寫入到這個 CLOB。  
  
## <a name="return-value"></a>傳回值  
 寫入的字元數。  
  
## <a name="exceptions"></a>例外狀況  
 java.sql.SQLException  
  
## <a name="remarks"></a>備註  
 這個 setString 方法是由 java.sql.Clob 介面中 setString 方法指定。  
  
 字元資料會從指定的位置開始覆寫，而且可以超過 CLOB 的初始長度。 指定位置 + 1 的值將會附加字串。 指定位置 + 2 或更大 (或是零或零以下) 的值將會擲回位置錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [setString 方法&#40;SQLServerClob&#41;](../../../connect/jdbc/reference/setstring-method-sqlserverclob.md)   
 [SQLServerClob 方法](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob 成員](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob 類別](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
