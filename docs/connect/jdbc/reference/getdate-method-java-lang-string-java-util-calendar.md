---
title: getDate 方法 (java.util.Calendar) 參數 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getDate (java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6d0deaf2-6f12-4a6e-b537-a51fa3478059
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e78dd5f0df9179e78da758da86548f5ab4b5038c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="getdate-method-javalangstring-javautilcalendar"></a>getDate 方法 (java.lang.String, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  在 Java 程式語言中使用指定的參數名稱和 Calendar 物件，擷取指定的參數值來當作 java.sql.Date 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Date getDate(java.lang.String sCol,  
                             java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>參數  
 *sCol*  
  
 包含參數名稱的**字串**。  
  
 *cal*  
  
 行事曆物件。  
  
## <a name="return-value"></a>傳回值  
 Date 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 GetDate 方法 java.sql.CallableStatement 介面中所指定此 getDate 方法。  
  
 這個方法會傳回有效日期部分[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]datetime 或 smalldatetime 資料型別，而時間部分是設定成 Java 時間基準 00:00 （午夜）。  
  
## <a name="see-also"></a>另請參閱  
 [getDate 方法&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getdate-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
