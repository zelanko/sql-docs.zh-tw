---
title: setCharacterStream 方法 (SQLServerClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.setCharacterStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c02778f2-6681-4a84-a58b-2bcfac4233e4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: da842fbc6240b072c7fe907aaa344d8d2ff1c6e7
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67974649"
---
# <a name="setcharacterstream-method-sqlserverclob"></a>setCharacterStream 方法 (SQLServerClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回資料流，此資料流將用於從給定位置開始將 Unicode 字元資料流寫入到 CLOB。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.io.Writer setCharacterStream(long pos)  
```  
  
#### <a name="parameters"></a>參數  
 *pos*  
  
 開始寫入 CLOB 物件的位置。  
  
## <a name="return-value"></a>傳回值  
 Unicode 編碼字元可寫入其中的資料流。  
  
## <a name="exceptions"></a>例外狀況  
 java.sql.SQLException  
  
## <a name="remarks"></a>備註  
 這個 setCharacterStream 方法是由 java.sql.Clob 介面中的 setCharacterStream 方法指定。  
  
 寫入器會從指定的位置開始覆寫 CLOB 中的字元資料，而且可以超過 CLOB 的初始長度。 指定位置 + 1 的值將會附加字元。 指定位置 + 2 或更大 (或是零或零以下) 的值將會擲回位置錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerClob 方法](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob 成員](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob 類別](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
