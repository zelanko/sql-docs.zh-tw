---
title: "getResponseBuffering 方法 (SQLServerDataSource) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDataSource.getResponseBuffering()
apilocation:
- SQLServerDataSource.getResponseBuffering()
apitype: Assembly
ms.assetid: 19585a93-88a4-415e-a20e-12ba58cddeaa
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0c278b31f870286f55d51a04dda2db4b43464ce4
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getresponsebuffering-method-sqlserverdatasource"></a>getResponseBuffering 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回的回應緩衝模式，這個[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.String getResponseBuffering()  
```  
  
## <a name="return-value"></a>傳回值  
 A**字串**可包含小寫**完整**或**適應性**。  
  
## <a name="remarks"></a>備註  
 **完整**值會指定在執行階段從伺服器讀取整個結果。  
  
 **適應性**值會指定緩衝處理最小可能的資料時所需。 **適應性**值是預設的緩衝模式。  
  
 如需使用回應緩衝模式的詳細資訊，請參閱[使用適應性緩衝](../../../connect/jdbc/using-adaptive-buffering.md)。  
  
## <a name="see-also"></a>另請參閱  
 [setResponseBuffering 方法 &#40;SQLServerDataSource &#41;](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverdatasource.md)   
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

