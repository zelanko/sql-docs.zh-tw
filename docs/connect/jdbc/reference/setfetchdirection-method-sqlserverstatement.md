---
title: setFetchDirection 方法 (SQLServerStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 18176517-2fb3-4266-924d-0f01253083d2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f3c6e0080f4d94b0d792c1994695c590fd4fed66
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47812336"
---
# <a name="setfetchdirection-method-sqlserverstatement"></a>setFetchDirection 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  提供 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 提示，作為處理結果集資料列時應遵循的方向。  
  
> [!NOTE]  
>  JDBC Driver 目前會忽略由這個方法所給定的提示。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setFetchDirection(int nDir)  
```  
  
#### <a name="parameters"></a>參數  
 *nDir*  
  
 指出資料列處理方向的 **int**，可能是下列其中一個值：  
  
 FETCH_FORWARD  
  
 FETCH_REVERSE  
  
 FETCH_UNKNOWN  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 setFetchDirection 方法是由 java.sql.Statement 介面中之 setFetchDirection 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
