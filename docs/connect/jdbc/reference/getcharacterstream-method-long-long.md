---
title: getCharacterStream 方法 (long，long) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d70f502f-f60f-436a-83e6-797a0ed71bf3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d875e82b4db5e1725f43307348d27a6701e2a88d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47697786"
---
# <a name="getcharacterstream-method-long-long"></a>getCharacterStream 方法 (long, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根據指定的位置和長度，傳回 **Clob** 資料作為 Reader 物件或字元資料流。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.io.Reader getCharacterStream(long pos,  
                                         long length)  
```  
  
#### <a name="parameters"></a>參數  
 *pos*  
  
 **long**，指出所要擷取部分值的第一個字元位移。  
  
 *length*  
  
 **long**，指出所要擷取部分值的字元長度。  
  
## <a name="return-value"></a>傳回值  
 讀取器物件，其中包含**Clob**資料。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getCharacterStream 方法是由 java.sql.Clob 介面中的 getCharacterStream 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [getCharacterStream 方法 &#40;SQLServerClob&#41;](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverclob.md)   
 [SQLServerClob 方法](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob 成員](../../../connect/jdbc/reference/sqlserverclob-members.md)  
  
  
