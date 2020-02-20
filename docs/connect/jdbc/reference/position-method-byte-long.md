---
title: position 方法 (byte, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerBlob.position (byte[], long)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 787412c2-4342-49c8-9ca2-7a9ddcd3277c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cf8cfa3bb6aed74c7689639698715dc24803d46d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67976471"
---
# <a name="position-method-byte-long"></a>position 方法 (byte, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  依據指定 **byte** 陣列模式和起始索引，傳回指定模式在 BLOB 中的位置。  
  
## <a name="syntax"></a>語法  
  
```  
  
public long position(byte[] bPattern,  
                     long start)  
```  
  
#### <a name="parameters"></a>參數  
 *bPattern*  
  
 要搜尋的模式。  
  
 *start*  
  
 搜尋所在的起始索引。  
  
## <a name="return-value"></a>傳回值  
 找到模式所在位置的 **long** 值，如果找不到，則為 -1。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 position 方法是由 java.sql.Blob 介面中的 position 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [position 方法 &#40;SQLServerBlob&#41;](../../../connect/jdbc/reference/position-method-sqlserverblob.md)   
 [SQLServerBlob 方法](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob 成員](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob 類別](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
