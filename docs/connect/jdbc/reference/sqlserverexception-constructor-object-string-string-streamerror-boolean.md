---
title: SQLServerException 建構函式 (java.lang.Object, java.lang.String, java.lang.String, StreamError, boolean) | Microsoft Docs
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
ms.openlocfilehash: 95217b384788ea78bd389948930ba34f580036ec
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80902614"
---
# <a name="sqlserverexception-constructor-javalangobject-javalangstring-javalangstring-streamerror-boolean"></a>SQLServerException 建構函式 (java.lang.Object, java.lang.String, java.lang.String, StreamError, boolean)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  當給定 [object](../../../connect/jdbc/reference/sqlserverexception-class.md)、**string** 物件、**string** 物件、**StreamError** 物件和 **boolean** 時，初始化 **SQLServerException** 類別的新執行個體。

## <a name="syntax"></a>語法  
  
```  

public SQLServerException(java.lang.Object obj,
            java.lang.String errText,
            java.lang.String errState,
            StreamError streamError,
            boolean bStack)

            
```  
  
#### <a name="parameters"></a>參數  
 *obj*  
  
 產生例外狀況的 IO 緩衝區。

 *errText*  
  
 包含錯誤文字的字串。
  
 *sqlState*  
  
 包含 SQL 狀態的列舉物件。
 
 *streamError*  
  
 包含錯誤詳細資料的 StreamError 物件。
 
 *bStack*  
  
 布林值，指出是否應該產生堆疊追蹤。
  
## <a name="see-also"></a>另請參閱  
 [SQLServerException 建構函式](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [SQLServerException 成員](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [SQLServerException 類別](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
