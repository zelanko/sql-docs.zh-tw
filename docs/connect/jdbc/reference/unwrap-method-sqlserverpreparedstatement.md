---
title: "unwrap 方法 (SQLServerPreparedStatement) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8e3ec950-3ac1-4c28-9e97-ddce3bd46578
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 85f008a4cf1135b1a0978d98bade8d2c99030629
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="unwrap-method-sqlserverpreparedstatement"></a>unwrap 方法 (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回物件，用於實作指定的介面，以允許存取[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-特有的方法。  
  
## <a name="syntax"></a>語法  
  
```  
  
public <T> T unwrap(Class<T> iface)  
```  
  
#### <a name="parameters"></a>參數  
 *iface*  
  
 類型的類別之**T**定義介面。  
  
## <a name="return-value"></a>傳回值  
 物件，可實作指定的介面。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 [Unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md)方法由 JDBC 4.0 規格中導入的 java.sql.Wrapper 介面所定義。  
  
 應用程式可能需要存取特有的 JDBC api 延伸模組[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]。 Unwrap 方法支援解除包裝成為這個物件可延伸，公用類別，在類別公開供應商延伸模組。  
  
 呼叫這個方法時，物件會解除包裝成為下列類別： [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)和[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)。  
  
 如需範例程式碼，請參閱[unwrap 方法 &#40;SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md).  
  
 如需詳細資訊，請參閱[包裝函式和介面](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
## <a name="see-also"></a>另請參閱  
 [isWrapperFor 方法 &#40;SQLServerPreparedStatement &#41;](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 成員](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 類別](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
