---
title: getFetchSize 方法 (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getFetchSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8115ca58-8ae9-46ce-8515-7905d7bb25fe
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 22ba06688fb402fdbcd5e9afd951a668ef9c440d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "67983203"
---
# <a name="getfetchsize-method-sqlserverstatement"></a>getFetchSize 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取結果集資料列數目，這個數目是從這個 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 物件所產生結果集物件的預設提取大小。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final int getFetchSize()  
```  
  
## <a name="return-value"></a>傳回值  
 **int**，指出 [setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverstatement.md) 方法所指定的提取大小。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getFetchSize 方法是由 java.sql.Statement 介面中的 getFetchSize 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
