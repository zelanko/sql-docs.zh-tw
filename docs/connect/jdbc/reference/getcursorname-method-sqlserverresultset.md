---
title: getCursorName 方法 (SQLServerResultSet) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getCursorName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e5b3af67-423a-4551-a4c6-a4bc076bd504
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a299f8505e279cc752670b92338c893aa6b9e13d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47624826"
---
# <a name="getcursorname-method-sqlserverresultset"></a>getCursorName 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取 SQL 資料指標的名稱，此資料指標由這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件使用。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 目前不支援這個方法。 如果呼叫這個方法，將擲回例外狀況。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.String getCursorName()  
```  
  
## <a name="return-value"></a>傳回值  
 包含資料指標的**字串**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getCursorName 方法是由 java.sql.ResultSet 介面中的 getCursorName 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
