---
description: getMoreResults 方法 ()
title: getMoreResults 方法 () | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: accbf0d6789b67b8ebd3998ead58fdbb949bd602
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88435380"
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
  
## <a name="remarks"></a>備註  
 此 getMoreResults 方法是由 java.sql.Statement 介面中的 getMoreResults 方法所指定。  
  
 呼叫 getMoreResults 方法會以隱含方式關閉目前開啟而且使用 [getResultSet](../../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md) 方法取得的任何結果集物件。  
  
## <a name="see-also"></a>另請參閱  
 [getMoreResults 方法 &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)   
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
