---
title: getDate 方法 (int) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getDate (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: aa9f08af-df24-4c80-8298-c4007339b20a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2e23755f9c1fd3df08103c7d463e87bf333c4b00
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47731446"
---
# <a name="getdate-method-int"></a>getDate 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  在 Java 程式語言中使用給定的參數索引，擷取指定之參數的值來當做 java.sql.Date 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Date getDate(int index)  
```  
  
#### <a name="parameters"></a>參數  
 *index*  
  
 指出參數索引的 **int**。  
  
## <a name="return-value"></a>傳回值  
 Date 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這項 getDate 方法由 java.sql.CallableStatement 介面中的 getDate 方法所指定。  
  
 這個方法會傳回 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **datetime** 或 **smalldatetime** 資料類型中的有效日期部分，而時間部分則會設定成 Java 時間基準 00:00 (午夜)。  
  
## <a name="see-also"></a>另請參閱  
 [getDate 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getdate-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
