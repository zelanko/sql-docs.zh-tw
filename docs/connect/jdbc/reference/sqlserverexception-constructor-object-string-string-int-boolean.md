---
description: SQLServerException 建構函式 (java.lang.Object, java.lang.String, java.lang.String, int, boolean)
title: SQLServerException 建構函式 (java.lang.Object, java.lang.String, java.lang.String, int, boolean) | Microsoft Docs
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
ms.openlocfilehash: f66bd8759733c2574438ba12ce9f12b00cf88842
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450482"
---
# <a name="sqlserverexception-constructor-javalangobject-javalangstring-javalangstring-int-boolean"></a>SQLServerException 建構函式 (java.lang.Object, java.lang.String, java.lang.String, int, boolean)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  當給定 **object**、**string** 物件、**string** 物件、**int** 與 **boolean** 時，初始化 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) 類別的新執行個體。

## <a name="syntax"></a>語法  
  
```  

public SQLServerException(java.lang.Object obj,
            java.lang.String errText,
            java.lang.String errState,
            int errNum,
            boolean bStack)

            
```  
  
#### <a name="parameters"></a>參數  
 *obj*  
  
 產生例外狀況的 IO 緩衝區。

 *errText*  
  
 包含錯誤文字的字串。
  
 *sqlState*  
  
 包含 SQL 狀態的列舉物件。
 
 *errNum*  
  
 int，其中包含例外狀況的錯誤碼。
 
 *bStack*  
  
 布林值，指出是否應該產生堆疊追蹤。
  
## <a name="see-also"></a>另請參閱  
 [SQLServerException 建構函式](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [SQLServerException 成員](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [SQLServerException 類別](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
