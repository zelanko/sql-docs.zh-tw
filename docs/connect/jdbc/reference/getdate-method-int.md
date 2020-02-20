---
title: getDate 方法 (int) | Microsoft Docs
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
ms.openlocfilehash: 2d959dc2f9372aa723089dc87bea66424c4d2ea8
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67984016"
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
  
## <a name="remarks"></a>備註  
 這項 getDate 方法由 java.sql.CallableStatement 介面中的 getDate 方法所指定。  
  
 這個方法會傳回 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **datetime** 或 **smalldatetime** 資料類型的有效日期部分，而時間部分則會設定成 Java 時間基準的 00:00 (午夜)。  
  
## <a name="see-also"></a>另請參閱  
 [getDate 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getdate-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
