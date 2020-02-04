---
title: getUnicodeStream 方法 (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getUnicodeStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0dd61865-663b-47e2-b417-e9df418894cc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 079663faa466b171df35481ee69374194c015acb
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67978387"
---
# <a name="getunicodestream-method-sqlserverresultset"></a>getUnicodeStream 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列中所指定資料行的值來當作 Unicode 字元資料流。  
  
> [!NOTE]  
>  JDBC 規格中已經取代這個方法，呼叫此方法將會擲回「未實作」例外狀況。 您應該改用 [getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) 方法。  
  
## <a name="overload-list"></a>多載清單  
  
|名稱|描述|  
|----------|-----------------|  
|[getUnicodeStream 方法 &#40;int&#41;](../../../connect/jdbc/reference/getunicodestream-method-int.md)|從這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件目前資料列中擷取所指定資料行索引的值來作為 Unicode 字元資料流。|  
|[getUnicodeStream 方法 &#40;java.lang.String&#41;](../../../connect/jdbc/reference/getunicodestream-method-java-lang-string.md)|從這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件目前資料列中擷取所指定資料行名稱的值來作為 Unicode 字元資料流。|  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
