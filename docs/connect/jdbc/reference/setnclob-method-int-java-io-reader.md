---
title: setNClob 方法 (int, java.io.Reader) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9fc9938c-b821-41c7-8df7-e21cb83a46d4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4abac6b892ae5960e8cafc5f265d6a81081e878b
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67973778"
---
# <a name="setnclob-method-int-javaioreader"></a>setNClob 方法 (int, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將指定的參數設定為所指定 Reader 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setNClob(int parameterIndex,  
                    java.io.Reader reader)  
```  
  
#### <a name="parameters"></a>參數  
 *parameterIndex*  
  
 指出參數索引的 **int**。  
  
 *reader*  
  
 Reader 物件，指出參數值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 setNClob 方法是由 java.sql.PreparedStatement 介面中的 setNClob 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [setNClob 方法 &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setnclob-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 成員](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
