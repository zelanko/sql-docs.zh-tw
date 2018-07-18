---
title: SQLServerClob 成員 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: Assembly
ms.assetid: 7db785ca-edd5-4833-8053-17fdbf87279a
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e81a9bb20fe94cdd1c51c6ed2fcaad3bf2704793
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32846793"
---
# <a name="sqlserverclob-members"></a>SQLServerClob 成員
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  下表列出所公開的成員[SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)類別。  
  
## <a name="constructors"></a>建構函式  
  
|名稱|Description|  
|----------|-----------------|  
|[SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-constructor-sqlserverconnection-java-lang-string.md)|初始化 SQLServerClob 類別的新執行個體。|  
  
## <a name="fields"></a>欄位  
 無。  
  
## <a name="inherited-fields"></a>繼承的欄位  
 無。  
  
## <a name="methods"></a>方法  
  
|名稱|Description|  
|----------|-----------------|  
|[可用](../../../connect/jdbc/reference/free-method-sqlserverclob.md)|這個方法會釋放 CLOB 物件並且釋出它所保留的資源。|  
|[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlserverclob.md)|具體化此 Clob 當做 ASCII 資料流。|  
|[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverclob.md)|傳回 Clob 資料當做 java.io.Reader 物件或字元資料流。|  
|[getSubString](../../../connect/jdbc/reference/getsubstring-method-sqlserverclob.md)|依據指定開始的位置和要複製的字元數目，傳回 Clob 中所指定子字串的副本。|  
|[長度](../../../connect/jdbc/reference/length-method-sqlserverclob.md)|傳回 Clob 中的字元數。|  
|[position](../../../connect/jdbc/reference/position-method-sqlserverclob.md)|依據指定的開始位置，傳回所指定 Clob 物件或 Clob 中之子字串的字元位置。|  
|[setAsciiStream](../../../connect/jdbc/reference/setasciistream-method-sqlserverclob.md)|傳回資料流，此資料流將用於從指定位置開始將 ASCII 字元寫入到這個 Clob。|  
|[setCharacterStream](../../../connect/jdbc/reference/setcharacterstream-method-sqlserverclob.md)|傳回資料流，此資料流將用於從指定位置開始將 Unicode 字元資料流寫入到這個 Clob。|  
|[setString](../../../connect/jdbc/reference/setstring-method-sqlserverclob.md)|從指定位置開始，寫入給定的字串到這個 Clob。|  
|[truncate](../../../connect/jdbc/reference/truncate-method-sqlserverclob.md)|截斷 Clob 成為指定的長度。|  
  
## <a name="inherited-methods"></a>繼承的方法  
  
|類別繼承自|方法|  
|--------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerClob 類別](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
