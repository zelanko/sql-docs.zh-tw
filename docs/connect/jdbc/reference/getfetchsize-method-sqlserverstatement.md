---
title: getFetchSize 方法 (SQLServerStatement) |Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 54869f3c689b0c493cdaf19b86f5d95a43835929
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66802015"
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
  
## <a name="remarks"></a>Remarks  
 這個 getFetchSize 方法是由 java.sql.Statement 介面中之 getFetchSize 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
