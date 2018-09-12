---
title: getDate 方法 (java.util.Calendar) 參數 |Microsoft Docs
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
ms.openlocfilehash: 535ffaaa4c4c302642c829c1995701fc89a500f2
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2018
ms.locfileid: "42787162"
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
  
 月曆物件。  
  
## <a name="return-value"></a>傳回值  
 Date 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getDate方法由 java.sql.CallableStatement 介面中的 getDate方法指定。  
  
 這個方法會傳回 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] datetime 或 smalldatetime 資料型別中的有效日期部分，而時間部分是設定成 Java 時間基準 (午夜 00:00)。  
  
## <a name="see-also"></a>另請參閱  
 [getDate 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getdate-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
