---
title: SQLServerNClob 成員 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b063f191-175e-4430-aab7-d88907f4ebec
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 81bcb5406a491d0e7b73ec098b160008c1a11c4a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47795536"
---
# <a name="sqlservernclob-members"></a>SQLServerNClob 成員
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  下表列出由 [SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md) 類別公開的成員。  
  
## <a name="constructors"></a>建構函式  
 無。  
  
## <a name="fields"></a>欄位  
 無。  
  
## <a name="inherited-fields"></a>繼承的欄位  
 無。  
  
## <a name="methods"></a>方法  
  
|[屬性]|Description|  
|----------|-----------------|  
|[free](../../../connect/jdbc/reference/free-method-sqlservernclob.md)|這個方法會釋放 **NCLOB** 物件並釋出它所保留的資源。|  
|[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlservernclob.md)|擷取**NCLOB**所指定值**java.sql.NClob**當做 ASCII 資料流的物件。|  
|[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlservernclob.md)|擷取**NCLOB**所指定值**java.sql.NClob**物件。|  
|[getSubString](../../../connect/jdbc/reference/getsubstring-method-sqlservernclob.md)|擷取在指定的子字串的複本**NCLOB**所指定值**java.sql.NClob**物件。|  
|[length](../../../connect/jdbc/reference/length-method-sqlservernclob.md)|擷取中的字元數目**NCLOB**所指定值**java.sql.NClob**物件。|  
|[position](../../../connect/jdbc/reference/position-method-sqlservernclob.md)|擷取指定的字元位置**java.sql.NClob**物件，或在子字串**java.sql.NClob**依據指定的開始位置。|  
|[setAsciiStream](../../../connect/jdbc/reference/setasciistream-method-sqlservernclob.md)|擷取資料流，此資料流將用於從指定位置開始，將 ASCII 字元寫入到這個 **java.sql.NClob** 物件所代表的 **NCLOB** 值。|  
|[setCharacterStream](../../../connect/jdbc/reference/setcharacterstream-method-sqlservernclob.md)|擷取資料流，此資料流將用於從指定位置開始，將 Unicode 字元資料流寫入到這個 **java.sql.NClob** 物件所代表的 **NCLOB** 值。|  
|[setString](../../../connect/jdbc/reference/setstring-method-sqlservernclob.md)|寫入指定**字串**要**NCLOB**指定位置開始。|  
|[truncate](../../../connect/jdbc/reference/truncate-method-sqlservernclob.md)|截斷 **NCLOB** 值成為指定的長度。|  
  
## <a name="inherited-methods"></a>繼承的方法  
  
|類別繼承自|方法|  
|--------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Clob|free, getAsciiStream, getCharacterStream, getSubString, length, position, setAsciiStream, setCharacterStream, setString, truncate|  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerClob 類別](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
