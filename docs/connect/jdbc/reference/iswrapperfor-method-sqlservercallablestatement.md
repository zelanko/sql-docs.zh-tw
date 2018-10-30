---
title: isWrapperFor 方法 (SQLServerCallableStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 71156863-3588-453e-b5a5-0573b2c1bebf
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 587c1217d42aa02c269b986837997dfbe89be278
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47737016"
---
# <a name="iswrapperfor-method-sqlservercallablestatement"></a>isWrapperFor 方法 (SQLServerCallableStatement)
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
 [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlservercallablestatement.md) 方法和 [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md) 方法是由 JDBC 4.0 中導入的 java.sql.Wrapper 介面所定義。  
  
 如果這個方法傳回 **true**，則配合相同引數呼叫 [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md) 將會成功。  
  
 如需詳細資訊，請參閱 <<c0> [ 包裝函式和介面](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
## <a name="see-also"></a>另請參閱  
 [unwrap 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
