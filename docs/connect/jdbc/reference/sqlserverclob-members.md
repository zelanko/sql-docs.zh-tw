---
title: SQLServerClob 成員 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apitype: Assembly
ms.assetid: 7db785ca-edd5-4833-8053-17fdbf87279a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 55e306b2fe7b8f52655f504d63f02ffc26e04ea1
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "67971778"
---
# <a name="sqlserverclob-members"></a>SQLServerClob 成員
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  下表列出由 [SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md) 類別公開的成員。  
  
## <a name="constructors"></a>建構函式  
  
|名稱|描述|  
|----------|-----------------|  
|[SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-constructor-sqlserverconnection-java-lang-string.md)|初始化 SQLServerClob 類別的新執行個體。|  
  
## <a name="fields"></a>欄位  
 無。  
  
## <a name="inherited-fields"></a>繼承的欄位  
 無。  
  
## <a name="methods"></a>方法  
  
|名稱|描述|  
|----------|-----------------|  
|[free](../../../connect/jdbc/reference/free-method-sqlserverclob.md)|這個方法會釋放 CLOB 物件並且釋出它所保留的資源。|  
|[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlserverclob.md)|具體化此 Clob 當做 ASCII 資料流。|  
|[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverclob.md)|傳回 Clob 資料當做 java.io.Reader 物件或字元資料流。|  
|[getSubString](../../../connect/jdbc/reference/getsubstring-method-sqlserverclob.md)|依據指定開始的位置和要複製的字元數目，傳回 Clob 中所指定子字串的副本。|  
|[length](../../../connect/jdbc/reference/length-method-sqlserverclob.md)|傳回 Clob 中的字元數。|  
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
  
  
