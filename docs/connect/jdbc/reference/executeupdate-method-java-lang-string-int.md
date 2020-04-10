---
title: executeUpdate 方法 (java.lang.String, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.executeUpdate (java.lang.String, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4c52a20e-527e-4d14-9a5a-4cd195aac8ed
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 10c248841bae87ba76834dd7bbee17ba38cf6647
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924321"
---
# <a name="executeupdate-method-javalangstring-int"></a>executeUpdate 方法 (java.lang.String, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  執行指定的 SQL 陳述式，並透過指定的旗標向 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 發出信號，通知是否要提供由這個 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 物件產生的自動產生索引鍵來進行擷取。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final int executeUpdate(java.lang.String sql,  
                               int flag)  
```  
  
#### <a name="parameters"></a>參數  
 *sql*  
  
 包含 SQL 陳述式的**字串**。  
  
 *旗標*  
  
 **int** 值，指出是否必須提供自動產生的索引鍵。 這個值一定是下面其中一個常數：  
  
 RETURN_GENERATED_KEYS  
  
 NO_GENERATED_KEYS  
  
## <a name="return-value"></a>傳回值  
 **int** 會指出受影響的資料列數目，如果是使用 DDL 陳述式，則為 0。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 executeUpdate 方法是由 java.sql.Statement interface 介面中的 executeUpdate 方法指定。  
  
 如果執行預存程序產生的更新計數大於一或是產生一個以上的結果集，請使用 [execute](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md) 方法執行預存程序。  
  
## <a name="see-also"></a>另請參閱  
 [executeUpdate 方法 &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)   
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
