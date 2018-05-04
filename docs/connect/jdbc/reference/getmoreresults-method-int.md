---
title: getMoreResults 方法 (int) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerStatement.getMoreResults (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6419e5a8-8b3a-4d5b-8226-95865c52c723
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 36a9cf3bfb2b6032694f9e33895b379bd83713ec
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="getmoreresults-method-int"></a>getMoreResults 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  移至下一步的結果[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件和處理任何目前開啟的結果集根據給定模式所指定的指示的物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final boolean getMoreResults(int mode)  
```  
  
#### <a name="parameters"></a>參數  
 *模式*  
  
 **Int** ，指出如何處理目前開啟的結果集物件。 必須是下面其中一個常數：  
  
 CLOSE_CURRENT_RESULT  
  
 KEEP_CURRENT_RESULT (JDBC 驅動程式不支援)  
  
 CLOSE_ALL_RESULTS  
  
## <a name="return-value"></a>傳回值  
 **true**如果傳回的結果是結果集。 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 GetMoreResults 方法 java.sql.Statement 介面中所指定此 getMoreResults 方法。  
  
 如果擷取結果之前呼叫 getMoreResults 方法，它的行為必須按照*模式*引數並移至下一個結果。  
  
> [!NOTE]  
>  JDBC 驅動程式不支援使用 KEEP_CURRENT_RESULT 常數。 如果使用此常數的話，將擲回例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [getMoreResults 方法&#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)   
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
