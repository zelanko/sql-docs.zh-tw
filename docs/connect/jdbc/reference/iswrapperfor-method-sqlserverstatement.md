---
title: isWrapperFor 方法 (SQLServerStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 53f3291f-d43a-476b-a656-d86168dacf6c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8bd0f84989a24c913ece143710e8f17055fa0171
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47798560"
---
# <a name="iswrapperfor-method-sqlserverstatement"></a>isWrapperFor 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指出這個陳述式物件是否為指定之介面的包裝函式。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean isWrapperFor(Class iface)  
```  
  
#### <a name="parameters"></a>參數  
 *iface*  
  
 A**類別**定義介面。  
  
## <a name="return-value"></a>傳回值  
 如果這個物件會實作介面或是會包裝實作此介面的物件，則為 **true**； 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) 方法和 [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) 方法是由 JDBC 4.0 中引進的 java.sql.Wrapper 介面所定義。  
  
 如果這個方法傳回 true，則搭配相同引數呼叫 [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) 將會成功。  
  
 如需範例程式碼，請參閱 <<c0> [ 更新大型資料範例](../../../connect/jdbc/updating-large-data-sample.md)。  
  
 如需詳細資訊，請參閱 <<c0> [ 包裝函式和介面](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
## <a name="see-also"></a>另請參閱  
 [unwrap 方法&#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)   
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
