---
title: setBinaryStream 方法 (SQLServerBlob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerBlob.setBinaryStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: abcec31f-1a60-4765-9725-8cf7e9f1f8ab
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4555dfb9256f3ffe2ba61e82fe90307991a5a580
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67975091"
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
 這個 setBinaryStream 方法是由 java.sql.Blob 介面中的 setBinaryStream 方法指定。  
  
 輸出資料流會從指定的位置開始覆寫 BLOB 中的資料，而且可以超過 BLOB 的初始長度。 指定位置 + 1 的值將會附加位元組。 傳遞位置 + 2 或更大 (或是零或零以下) 的值將會擲回位置錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerBlob 方法](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob 成員](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob 類別](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
