---
title: isWrapperFor 方法 (SQLServerPreparedStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b0e591b1-73e2-4f90-967f-5555eadfc3f1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 37d08855ff496811c82b39aa19fc05d85864d9b3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47627989"
---
# <a name="iswrapperfor-method-sqlserverpreparedstatement"></a>isWrapperFor 方法 (SQLServerPreparedStatement)
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
 如果這個物件會實作介面或是會包裝實作此介面的物件，則為 **true**。 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverpreparedstatement.md) 方法和 [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md) 方法是由已自 JDBC 4.0 規格中導入的 java.sql.Wrapper 介面所定義。  
  
 如果這個方法傳回 true，則配合相同引數呼叫 [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md) 將會成功。  
  
 如需詳細資訊，請參閱 <<c0> [ 包裝函式和介面](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
## <a name="see-also"></a>另請參閱  
 [unwrap 方法 &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 成員](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 類別](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
