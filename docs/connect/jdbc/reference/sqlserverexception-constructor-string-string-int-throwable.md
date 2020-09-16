---
description: SQLServerException 建構函式 (java.lang.String、java.lang.String、int、java.lang.Throwable)
title: SQLServerException 建構函式 (java.lang.String、java.lang.String、int、java.lang.Throwable) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fb84d0c1216047f28ed980806129ff1e21c08bb6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450432"
---
# <a name="sqlserverexception-constructor-javalangstring-javalangstring-int-javalangthrowable"></a>SQLServerException 建構函式 (java.lang.String、java.lang.String、int、java.lang.Throwable)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  當提供 **string** 物件、**string** 物件、**int**，以及 **throwable** 物件時，初始化 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) 類別的新執行個體。

## <a name="syntax"></a>語法  
  
```  
public SQLServerException(java.lang.String errText,
            SQLState errState,
            int errNum,
            java.lang.Throwable cause)
            
```  
  
#### <a name="parameters"></a>參數  
 *errText*  
  
 包含錯誤文字的字串。
  
 *errState*  
  
 包含錯誤狀態的字串。
 
 *errNum*  
  
 包含例外狀況之錯誤碼的 int。
 
 *cause*  
  
 包含例外狀況原因的 throwable 物件。
  
## <a name="see-also"></a>另請參閱  
 [SQLServerException 建構函式](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [SQLServerException 成員](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [SQLServerException 類別](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
