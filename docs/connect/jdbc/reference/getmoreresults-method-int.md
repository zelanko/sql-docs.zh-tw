---
title: getMoreResults 方法 (int) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getMoreResults (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6419e5a8-8b3a-4d5b-8226-95865c52c723
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 08760680774b2e760b66d9e210c4ef939872444e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67981772"
---
# <a name="getmoreresults-method-int"></a>getMoreResults 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  移至這個 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 物件的下一個結果，並根據指定模式所指定的指示來處理目前開啟的任何結果集物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final boolean getMoreResults(int mode)  
```  
  
#### <a name="parameters"></a>參數  
 *mode*  
  
 **int**，指出如何處理目前開啟的結果集物件。 必須是下面其中一個常數：  
  
 CLOSE_CURRENT_RESULT  
  
 KEEP_CURRENT_RESULT (JDBC 驅動程式不支援)  
  
 CLOSE_ALL_RESULTS  
  
## <a name="return-value"></a>傳回值  
 如果傳回的結果是結果集，則為 **true**； 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getMoreResults 方法是由 sql 語句介面中的 getMoreResults 方法指定。  
  
 如果在擷取結果之前呼叫 getMoreResults 方法，它的行為會如同 *mode* 引數所指定，並移到下一個結果。  
  
> [!NOTE]  
>  JDBC 驅動程式不支援使用 KEEP_CURRENT_RESULT 常數。 如果使用此常數的話，將擲回例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [getMoreResults 方法 &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)   
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
