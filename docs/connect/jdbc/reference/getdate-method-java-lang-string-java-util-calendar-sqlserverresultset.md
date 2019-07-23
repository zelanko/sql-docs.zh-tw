---
title: getDate 方法 (util) 資料行 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getDate (java.lang.String, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3fa2a72a-7499-44ec-8f76-a8e646e0190c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 36c1a84fe690760d6eeda6b43fb59a5d0268696c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67984003"
---
# <a name="getdate-method-javalangstring-javautilcalendar-sqlserverresultset"></a>getDate 方法 (java.lang.String, java.util.Calendar) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用Java 程式設計語言，透過指定的 Calender 物件，從 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的目前資料列內擷取指定資料行名稱值作為 java.sql.Date 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Date getDate(java.lang.String colName,  
                             java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>參數  
 *colName*  
  
 包含資料行名稱的**字串**。  
  
 *cal*  
  
 行事曆物件。  
  
## <a name="return-value"></a>傳回值  
 Date 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getDate 方法是由 java.sql.ResultSet 介面中的 getDate 方法指定。  
  
 這個方法會傳回 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] datetime 或 smalldatetime 資料類型中的有效日期部分，而時間部分會根據所提供的 Calendar 時區設定成 Java 時間基準 00:00 (午夜)。  
  
## <a name="see-also"></a>另請參閱  
 [getDate 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getdate-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
