---
title: getQueryTimeout 方法 (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getQueryTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8dff954f-b458-4fa6-abe6-be62ff75e2b9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 03f1833cff6bb65551c4a9c02dd72cb758a555c4
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925180"
---
# <a name="getquerytimeout-method-sqlserverstatement"></a>getQueryTimeout 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 將等候這個 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 物件執行的秒數。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final int getQueryTimeout()  
```  
  
## <a name="return-value"></a>傳回值  
 **int**，指出 JDBC 驅動程式將等候的秒數，如果沒有任何限制，則為 0。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getQueryTimeout 方法是由 java.sql.Statement 介面中的 getQueryTimeout 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
