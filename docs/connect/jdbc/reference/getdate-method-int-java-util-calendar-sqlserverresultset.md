---
title: getDate 方法 (int, java.util.Calendar) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getDate (int, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 150411f7-2a73-4380-b921-9698acd5d1f9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a9edc9762a1d75c90c5fb1c9564766eb38da0421
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47773676"
---
# <a name="getdate-method-int-javautilcalendar-sqlserverresultset"></a>getDate 方法 (int, java.util.Calendar) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用 Java 程式設計語言，並透過指定 Calendar 物件，擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列中指定資料行索引的值來當作 java.sql.Date 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Date getDate(int columnIndex,  
                             java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>參數  
 *columnIndex*  
  
 指出資料行索引的 **int**。  
  
 *cal*  
  
 月曆物件。  
  
## <a name="return-value"></a>傳回值  
 Date 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getDate 方法是由 java.sql.ResultSet 介面中的 getDate 方法指定。  
  
 這個方法會傳回 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] datetime 或 smalldatetime 資料類型中的有效日期部分，而時間部分會根據所提供的 Calendar 時區設定成 Java 時間基準 00:00 (午夜)。  
  
## <a name="see-also"></a>另請參閱  
 [getDate 方法&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getdate-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
