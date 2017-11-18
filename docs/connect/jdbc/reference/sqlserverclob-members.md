---
title: "SQLServerClob 成員 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apitype: Assembly
ms.assetid: 7db785ca-edd5-4833-8053-17fdbf87279a
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 41909851b81767272d50a4d93426bcdc4dbb075f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

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
|[釋放](../../../connect/jdbc/reference/free-method-sqlserverclob.md)|這個方法會釋放 CLOB 物件並且釋出它所保留的資源。|  
|[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlserverclob.md)|具體化此 Clob 當做 ASCII 資料流。|  
|[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverclob.md)|傳回 Clob 資料當做 java.io.Reader 物件或字元資料流。|  
|[getSubString](../../../connect/jdbc/reference/getsubstring-method-sqlserverclob.md)|依據指定開始的位置和要複製的字元數目，傳回 Clob 中所指定子字串的副本。|  
|[長度](../../../connect/jdbc/reference/length-method-sqlserverclob.md)|傳回 Clob 中的字元數。|  
|[位置](../../../connect/jdbc/reference/position-method-sqlserverclob.md)|依據指定的開始位置，傳回所指定 Clob 物件或 Clob 中之子字串的字元位置。|  
|[setAsciiStream](../../../connect/jdbc/reference/setasciistream-method-sqlserverclob.md)|傳回資料流，此資料流將用於從指定位置開始將 ASCII 字元寫入到這個 Clob。|  
|[setCharacterStream](../../../connect/jdbc/reference/setcharacterstream-method-sqlserverclob.md)|傳回資料流，此資料流將用於從指定位置開始將 Unicode 字元資料流寫入到這個 Clob。|  
|[setString](../../../connect/jdbc/reference/setstring-method-sqlserverclob.md)|從指定位置開始，寫入給定的字串到這個 Clob。|  
|[截斷](../../../connect/jdbc/reference/truncate-method-sqlserverclob.md)|截斷 Clob 成為指定的長度。|  
  
## <a name="inherited-methods"></a>繼承的方法  
  
|類別繼承自|方法|  
|--------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerClob 類別](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  

