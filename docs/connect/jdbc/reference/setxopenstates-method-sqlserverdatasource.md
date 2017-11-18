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
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDataSource.setXopenStates
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9723591f-e987-426f-b70a-07f5c70dc094
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 857d9f914e10365746381ee4335f35f19d4beedd
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

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
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

