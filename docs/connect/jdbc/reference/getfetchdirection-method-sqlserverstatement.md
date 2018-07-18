---
title: getFetchDirection 方法 (SQLServerStatement) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerStatement.getFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ceb4ae68-decc-46d3-83f1-0bbd23aaf58c
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ce1a90324b0cc7fd40e22b0cb90537b985f3d754
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32834233"
---
# <a name="getfetchdirection-method-sqlserverstatement"></a>getFetchDirection 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取從資料庫資料表擷取資料列是從這個所產生的結果集的預設值的方向[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件。  
  
> [!NOTE]  
>  這個方法目前尚未實作所[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]。 因此，它一定會傳回 FETCH_UNKNOWN。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final int getFetchDirection()  
```  
  
## <a name="return-value"></a>傳回值  
 **Int** ，指出所指定的提取方向[setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverstatement.md)方法。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 GetFetchDirection 方法 java.sql.Statement 介面中所指定此 getFetchDirection 方法。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
