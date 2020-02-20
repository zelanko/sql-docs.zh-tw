---
title: SQLServerNClob 成員 | Microsoft Docs
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
ms.openlocfilehash: 303742b8e7b7bf8221565e09cf23d2e18cdca8de
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67970941"
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
  
|名稱|描述|  
|----------|-----------------|  
|[free](../../../connect/jdbc/reference/free-method-sqlservernclob.md)|這個方法會釋放 **NCLOB** 物件並釋出它所保留的資源。|  
|[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlservernclob.md)|將 **java.sql.NClob** 物件所指定的 **NCLOB** 值擷取為 ASCII 資料流。|  
|[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlservernclob.md)|擷取由 **java.sql.NClob** 物件所指定的 **NCLOB** 值。|  
|[getSubString](../../../connect/jdbc/reference/getsubstring-method-sqlservernclob.md)|擷取由 **java.sql.NClob** 物件所指定 **NCLOB** 值中的指定子字串副本。|  
|[length](../../../connect/jdbc/reference/length-method-sqlservernclob.md)|擷取由 **java.sql.NClob** 物件所指定 **NCLOB** 值中的字元數。|  
|[position](../../../connect/jdbc/reference/position-method-sqlservernclob.md)|依據指定的開始位置，擷取所指定 **java.sql.NClob** 物件或 **java.sql.NClob** 中子字串的字元位置。|  
|[setAsciiStream](../../../connect/jdbc/reference/setasciistream-method-sqlservernclob.md)|擷取資料流，此資料流將用於從指定位置開始，將 ASCII 字元寫入到這個 **java.sql.NClob** 物件所代表的 **NCLOB** 值。|  
|[setCharacterStream](../../../connect/jdbc/reference/setcharacterstream-method-sqlservernclob.md)|擷取資料流，此資料流將用於從指定位置開始，將 Unicode 字元資料流寫入到這個 **java.sql.NClob** 物件所代表的 **NCLOB** 值。|  
|[setString](../../../connect/jdbc/reference/setstring-method-sqlservernclob.md)|從指定位置開始將指定 **String** 寫入 **NCLOB**。|  
|[truncate](../../../connect/jdbc/reference/truncate-method-sqlservernclob.md)|截斷 **NCLOB** 值成為指定的長度。|  
  
## <a name="inherited-methods"></a>繼承的方法  
  
|類別繼承自|方法|  
|--------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Clob|free, getAsciiStream, getCharacterStream, getSubString, length, position, setAsciiStream, setCharacterStream, setString, truncate|  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerClob 類別](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
