---
title: "getResponseBuffering 方法 (SQLServerStatement) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerStatement.getResponseBuffering()
apilocation: SQLServerStatement.getResponseBuffering()
apitype: Assembly
ms.assetid: a9a9ffdd-7ce3-4e0a-907c-34d6a54e6865
caps.latest.revision: "23"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d9c2211fdba2431751d4c33ece8061af2681af90
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="getresponsebuffering-method-sqlserverstatement"></a>getResponseBuffering 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取的回應緩衝模式，這個[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final java.lang.String getResponseBuffering()  
```  
  
## <a name="return-value"></a>傳回值  
 A**字串**可包含小寫**完整**或**適應性**。  
  
## <a name="remarks"></a>備註  
 **自動調整**指定最小可能的資料在必要時緩衝處理。  
  
 **完整**指定在執行階段從伺服器讀取整個結果。  
  
 **自動調整**是 JDBC Driver 2.0 和 3.0 版中的預設值。 **完整**是 JDBC Driver 2.0 版之前的預設值。  
  
 如需使用回應緩衝模式的詳細資訊，請參閱[使用適應性緩衝](../../../connect/jdbc/using-adaptive-buffering.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [setResponseBuffering 方法 &#40;SQLServerStatement &#41;](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)   
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
