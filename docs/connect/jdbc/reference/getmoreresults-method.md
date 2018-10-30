---
title: getMoreResults 方法 （) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getMoreResults ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: df89db50-0b2f-4094-820a-30be25ad72fe
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f2a0b2994bf377610574efbd5c3ff78b0d55035d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47718366"
---
# <a name="getmoreresults-method-"></a>getMoreResults 方法 ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  移至這個 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 物件的下一個結果。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final boolean getMoreResults()  
```  
  
## <a name="return-value"></a>傳回值  
 如果傳回的結果是結果集，則為 **true**； 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 GetMoreResults 方法 java.sql.Statement 介面中所指定這個 getMoreResults 方法。  
  
 呼叫 getMoreResults 方法會以隱含方式關閉目前開啟而且使用 [getResultSet](../../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md) 方法取得的任何結果集物件。  
  
## <a name="see-also"></a>另請參閱  
 [getMoreResults 方法 &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)   
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
