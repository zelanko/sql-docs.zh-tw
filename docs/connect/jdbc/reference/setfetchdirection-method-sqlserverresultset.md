---
title: setFetchDirection 方法 (SQLServerResultSet) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.setFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4ee82290-508d-4bff-a5c5-8a56338deef8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e725eb2bf07c587d04cf660917b9d0b70bf5cff3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47695816"
---
# <a name="setfetchdirection-method-sqlserverresultset"></a>setFetchDirection 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  提供提示，作為將處理這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中資料列的方向。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 目前不支援這個方法。 當您使用這個方法時，JDBC Driver 會記住設定，但是不會立刻執行。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setFetchDirection(int direction)  
```  
  
#### <a name="parameters"></a>參數  
 *direction*  
  
 **int**，指出建議的提取方向。 可以是下列其中一個值：  
  
 ResultSet.FETCH_FORWARD  
  
 ResultSet.FETCH_REVERSE  
  
 ResultSet.FETCH_UNKNOWN  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 setFetchDirection 方法是由 java.sql.ResultSet 介面中之 setFetchDirection 方法指定。  
  
 這個方法的初始值，是由產生此 SQLServerResultSet 物件的 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 物件所決定。 提取方向可以隨時變更。  
  
> [!NOTE]  
>  當資料指標類型為順向時，使用這個方法不會產生任何作用。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
