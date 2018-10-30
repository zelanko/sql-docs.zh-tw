---
title: setAsciiStream 方法 (SQLServerClob) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.setAsciiStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6e1779df-3b2a-41d1-8dca-99692cc9da14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a93a6a8750f48f58c6e676ebe619985dad67277d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47694806"
---
# <a name="setasciistream-method-sqlserverclob"></a>setAsciiStream 方法 (SQLServerClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回資料流，此資料流將用於從給定位置開始將 ASCII 字元寫入到 CLOB。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.io.OutputStream setAsciiStream(long pos)  
```  
  
#### <a name="parameters"></a>參數  
 *pos*  
  
 開始寫入 CLOB 物件的位置。  
  
## <a name="return-value"></a>傳回值  
 ASCII 編碼字元可寫入其中的資料流。  
  
## <a name="exceptions"></a>例外狀況  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 這個 setAsciiStream 方法是由 java.sql.Clob 介面中的 setAsciiStream 方法指定。  
  
 輸出資料流會從給定位置開始覆寫 CLOB 中的字元資料，而且可以超過 CLOB 的初始長度。 指定位置 + 1 的值將會附加 ASCII 字元。 指定位置 + 2 或更大 (或是零或零以下) 的值將會擲回位置錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerClob 方法](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob 成員](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob 類別](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
