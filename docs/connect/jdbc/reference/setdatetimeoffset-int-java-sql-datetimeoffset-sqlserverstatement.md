---
title: setDateTimeOffset （int，java.sql.DateTimeOffset） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e8b6e380-6b53-489b-be73-73fcb5258269
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 722250967bca8484f359d1e33a7541d34eb3ac79
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="setdatetimeoffsetint-javasqldatetimeoffset-sqlserverstatement"></a>setDateTimeOffset(int, java.sql.DateTimeOffset) (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將指定的參數設定為給定的 DateTimeOffset 值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setDateTimeOffset(int parameterIndex, DateTimeOffset dateTime)  
```  
  
#### <a name="parameters"></a>參數  
 *parameterIndex*  
  
 要設定之資料行的索引。  
  
 *DateTimeOffset*  
  
 DateTimeOffset 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 DateTimeOffset 格式為 "YYYY-MM-DD HH-MM-SS[.nnnnnnn] [+][-] HH:MM"。 使用下表當做參考。  
  
|SQL 型別|Insert|  
|--------------|------------|  
|datetime|只能插入："YYYY-MM-DD hh:mm:ss[.nnn]"|  
|smalldatetime|只能插入："YYYY-MM-DD hh:mm:ss"|  
|Time|只能插入："hh:mm:ss[.nnnnnnn]"|  
|日期|只能插入："YYYY-MM-DD"|  
|datetime2|只能插入："YYYY-MM-DD hh:mm:ss[.nnnnnnn]"|  
  
## <a name="see-also"></a>另請參閱  
 [getDateTimeOffset &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getdatetimeoffset-sqlserverresultset.md)   
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
