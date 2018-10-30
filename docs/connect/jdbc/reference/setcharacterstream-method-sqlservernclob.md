---
title: setCharacterStream 方法 (SQLServerNClob) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 09042ee9-dfb1-4d0b-82bd-d1224b0aea80
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 081da23826951c5c8c4d4872de1c28a771a2958b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47720916"
---
# <a name="setcharacterstream-method-sqlservernclob"></a>setCharacterStream 方法 (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取資料流，此資料流將用於從指定位置開始，將 Unicode 字元資料流寫入到這個 **java.sql.NClob** 物件所代表的 **NCLOB** 值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.io.Writer setCharacterStream(long pos)  
```  
  
#### <a name="parameters"></a>參數  
 *pos*  
  
 開始寫入至 **NCLOB** 值的位置，第一個位置是 1。  
  
## <a name="return-value"></a>傳回值  
 Writer 物件，表示 Unicode 編碼字元可寫入其中的資料流。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 setCharacterStream 方法 setCharacterStream 方法 java.sql.NClob 介面中所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerNClob 方法](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [SQLServerNClob 成員](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [SQLServerNClob 類別](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
