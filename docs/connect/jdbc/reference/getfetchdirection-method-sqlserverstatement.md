---
title: getFetchDirection 方法 (SQLServerStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ceb4ae68-decc-46d3-83f1-0bbd23aaf58c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3944990d8b6f551ba70545e5cacf42179e7b68ec
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47617086"
---
# <a name="getfetchdirection-method-sqlserverstatement"></a>getFetchDirection 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取從資料庫資料表中提取資料列的方向，此方向是從這個 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 物件所產生結果集的預設值。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 目前不會實作這個方法。 因此，它一定會傳回 FETCH_UNKNOWN。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final int getFetchDirection()  
```  
  
## <a name="return-value"></a>傳回值  
 **int**，指出由 [setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverstatement.md) 方法指定的提取方向。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getFetchDirection 方法是由 java.sql.Statement 介面中的 getFetchDirection 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
