---
title: setFetchSize 方法 (SQLServerStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setFetchSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 760e555e-9667-4b40-b0ba-778026ff2923
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: acf74ae4b3f9c95002de418a5b77a44a7b0a1bfa
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66764600"
---
# <a name="setfetchsize-method-sqlserverstatement"></a>setFetchSize 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  提供 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 提示，作為在需要更多資料列時應該從資料庫中提取的資料列數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setFetchSize(int rows)  
```  
  
#### <a name="parameters"></a>參數  
 *rows*  
  
 **int**，指出所要提取資料列的數目。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 setFetchSize 方法是由 java.sql.Statement 介面中的 setFetchSize 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
