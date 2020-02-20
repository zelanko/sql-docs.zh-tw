---
title: setByte 方法 (SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setByte
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 39c5ca20-d5f0-40dd-a853-29c3b8cd38e8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 410d42a5fa7fdf0e1b3415f85214a87af993b7db
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67974983"
---
# <a name="setbyte-method-sqlserverpreparedstatement"></a>setByte 方法 (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將指定的參數設定為所指定 **byte** 值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setByte(int n,  
                          byte x)  
```  
  
#### <a name="parameters"></a>參數  
 *n*  
  
 **int**，指出參數編號。  
  
 *x*  
  
 **byte** 值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 setByte 方法是由 java.sql.PreparedStatement 介面中的 setByte 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerPreparedStatement 成員](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 類別](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
