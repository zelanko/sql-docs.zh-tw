---
title: "setXopenStates 方法 (SQLServerDataSource) |Microsoft 文件"
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
apiname: SQLServerDataSource.setXopenStates
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 9723591f-e987-426f-b70a-07f5c70dc094
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bb9d14bebdbb8f6d7e2569cd5081541ca9080431
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="setxopenstates-method-sqlserverdatasource"></a>setXopenStates 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定**布林**值，指出是否啟用將 SQL 狀態轉換成 XOPEN 標準狀態。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setXopenStates(boolean xopenStates)  
```  
  
#### <a name="parameters"></a>參數  
 *xopenStates*  
  
 **true**如果啟用將 SQL 狀態轉換成 XOPEN 標準狀態。 否則為 **false**。  
  
## <a name="remarks"></a>備註  
 如果 xopenStates 屬性設定為**true**、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]會將 SQL 狀態轉換成 XOPEN 標準狀態。 預設值是**false**，因而導致 JDBC 驅動程式來產生 SQL 99 狀態碼。 如果 xopenStates 未設定， [getXopenStates](../../../connect/jdbc/reference/getxopenstates-method-sqlserverdatasource.md)方法會傳回預設值**false**。  
  
## <a name="see-also"></a>請參閱＜  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
