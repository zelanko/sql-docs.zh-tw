---
title: setDate 方法設定為 date 和 calendar - string | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setDate (java.lang.String, java.sql.Date, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fd152ad6-dd5e-49ef-b166-917371a2cba6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0f986b7fd5faadfbd24708ec9a339d3bd2f104f0
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67974575"
---
# <a name="setdate-method-javalangstring-javasqldate-javautilcalendar"></a>setDate 方法 (java.lang.String, java.sql.Date, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將指定的參數設定為給定的日期和行事曆值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setDate(java.lang.String sCol,  
                    java.sql.Date x,  
                    java.util.Calendar c)  
```  
  
#### <a name="parameters"></a>參數  
 *n*  
  
 **int**，指出參數編號。  
  
 *x*  
  
 Date 物件。  
  
 *c*  
  
 Calendar 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 setDate 方法是由 java.sql.CallableStatement 介面中的 setDate 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
