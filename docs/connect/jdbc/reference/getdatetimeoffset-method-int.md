---
title: "getDateTimeOffset 方法 (int) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8bb00356-4d6e-4625-b924-67646930fdf2
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3171789255d0184715917429c7627aadd734d62e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getdatetimeoffset-method-int"></a>getDateTimeOffset 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  這個方法加入在[!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC 驅動程式 3.0。  
  
 擷取所指定之參數的值[DateTimeOffset 類別](../../../connect/jdbc/reference/datetimeoffset-class.md)Java 程式語言中使用給定的參數索引中的物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public microsoft.sql.DateTimeOffset getDateTimeOffset(int index)  
```  
  
#### <a name="parameters"></a>參數  
 *索引*  
  
 以一為基底的參數序數。  
  
## <a name="return-value"></a>傳回值  
 A [DateTimeOffset 類別](../../../connect/jdbc/reference/datetimeoffset-class.md)物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 您可以設定[DateTimeOffset 類別](../../../connect/jdbc/reference/datetimeoffset-class.md)參數值與[SQLServerCallableStatement.setDateTimeOffset](../../../connect/jdbc/reference/setdatetimeoffset-method-sqlservercallablestatement.md)。  
  
## <a name="see-also"></a>另請參閱  
 [getDateTimeOffset 方法 &#40;SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getdatetimeoffset-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

