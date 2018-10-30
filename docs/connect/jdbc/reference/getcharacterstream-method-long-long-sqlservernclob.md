---
title: getCharacterStream 方法 (long, long) (SQLServerNClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5a8028bc-c877-4668-b662-0746d462040e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5071cf1e570418723ced2602f6b88a5a2227069c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47633616"
---
# <a name="getcharacterstream-method-long-long-sqlservernclob"></a>getCharacterStream 方法 (long, long) (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根據指定的位置和長度，擷取 **NCLOB** 資料作為 **Reader** 物件或字元資料流。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.io.Reader getCharacterStream(long pos,  
                                  long length)  
```  
  
#### <a name="parameters"></a>參數  
 *pos*  
  
 **long**，指出將擷取之部分值之第一個字元的位移。  
  
 *length*  
  
 **long**，指出將擷取的部分值字元長度。  
  
## <a name="return-value"></a>傳回值  
 包含 **NCLOB** 資料的 Reader 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 GetCharacterStream 方法 java.sql.NClob 介面中所指定這個 getCharacterStream 方法。  
  
## <a name="see-also"></a>另請參閱  
 [getCharacterStream 方法 &#40;SQLServerNClob&#41;](../../../connect/jdbc/reference/getcharacterstream-method-sqlservernclob.md)   
 [SQLServerNClob 方法](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [SQLServerNClob 成員](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [SQLServerNClob 類別](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
