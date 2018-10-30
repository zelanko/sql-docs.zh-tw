---
title: getConcurrency 方法 (SQLServerResultSet) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getConcurrency
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 207e25f4-769c-4ff3-913c-3517b06208e4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6daf6d4d9f4c0d9ec018a9a1ff135760d64b63e7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47795726"
---
# <a name="getconcurrency-method-sqlserverresultset"></a>getConcurrency 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的並行模式。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getConcurrency()  
```  
  
## <a name="return-value"></a>傳回值  
 指出並行類型的 **int**，可能是下列其中一個值：  
  
 ResultSet.CONCUR_READ_ONLY  
  
 ResultSet.CONCUR_UPDATABLE  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getConcurrency 方法是由 java.sql.ResultSet 介面中的 getConcurrency 方法指定。  
  
 使用的並行是由建立結果集的 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 物件所決定。  
  
 這個方法可用來決定實際的並行。 如果應用程式選取 CONCUR_READ_ONLY 或 CONCUR_UPDATABLE，將會傳回這些項目。 如果應用程式使用預設並行，將會傳回 CONCUR_READ_ONLY。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
