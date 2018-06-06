---
title: SQLServerNClob 成員 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b063f191-175e-4430-aab7-d88907f4ebec
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 55bc36ca4d6bcf6337598ddf6ec6ea8bb905dae2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqlservernclob-members"></a>SQLServerNClob 成員
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  下表列出所公開的成員[SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)類別。  
  
## <a name="constructors"></a>建構函式  
 無。  
  
## <a name="fields"></a>欄位  
 無。  
  
## <a name="inherited-fields"></a>繼承的欄位  
 無。  
  
## <a name="methods"></a>方法  
  
|名稱|Description|  
|----------|-----------------|  
|[可用](../../../connect/jdbc/reference/free-method-sqlservernclob.md)|這個方法會釋放**NCLOB**物件並釋出它所保留的資源。|  
|[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlservernclob.md)|擷取**NCLOB**值由所指定**java.sql.NClob**當做 ASCII 資料流的物件。|  
|[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlservernclob.md)|擷取**NCLOB**值由所指定**java.sql.NClob**物件。|  
|[getSubString](../../../connect/jdbc/reference/getsubstring-method-sqlservernclob.md)|擷取在指定的子字串副本**NCLOB**值由所指定**java.sql.NClob**物件。|  
|[長度](../../../connect/jdbc/reference/length-method-sqlservernclob.md)|擷取中的字元數**NCLOB**值由所指定**java.sql.NClob**物件。|  
|[position](../../../connect/jdbc/reference/position-method-sqlservernclob.md)|擷取指定的字元位置**java.sql.NClob**物件或子字串中**java.sql.NClob**依據指定的開始位置。|  
|[setAsciiStream](../../../connect/jdbc/reference/setasciistream-method-sqlservernclob.md)|擷取要用於寫入 ASCII 資料流字元**NCLOB**值**java.sql.NClob**物件表示，從指定位置開始。|  
|[setCharacterStream](../../../connect/jdbc/reference/setcharacterstream-method-sqlservernclob.md)|擷取要用來寫入到 Unicode 字元資料流的資料流**NCLOB**值**java.sql.NClob**物件表示，從指定位置開始。|  
|[setString](../../../connect/jdbc/reference/setstring-method-sqlservernclob.md)|寫入指定**字串**至**NCLOB**指定位置開始。|  
|[truncate](../../../connect/jdbc/reference/truncate-method-sqlservernclob.md)|會截斷**NCLOB**為指定之長度的值。|  
  
## <a name="inherited-methods"></a>繼承的方法  
  
|類別繼承自|方法|  
|--------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Clob|free, getAsciiStream, getCharacterStream, getSubString, length, position, setAsciiStream, setCharacterStream, setString, truncate|  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerClob 類別](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
