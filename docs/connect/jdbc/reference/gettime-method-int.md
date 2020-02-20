---
title: getTime 方法 (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getTime (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6c13dea2-511f-48dc-b3db-2d3b72ccc9de
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6e0426a89de1e3cf78f1f41e45fc35ba81816362
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67979091"
---
# <a name="gettime-method-int"></a>getTime 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  在 Java 程式語言中使用給定的參數索引，擷取指定之參數的值來當做 java.sql.Time 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Time getTime(int index)  
```  
  
#### <a name="parameters"></a>參數  
 *index*  
  
 指出參數索引的 **int**。  
  
## <a name="return-value"></a>傳回值  
 Time 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這項 getTime 方法由 java.sql.CallableStatement 介面中的 getTime 方法指定。  
  
 請參閱[了解資料類型轉換](../../../connect/jdbc/understanding-data-type-conversions.md)中標題為「Getter 方法轉換」的圖表，以查看可以使用此方法擷取哪些 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型。  
  
## <a name="see-also"></a>另請參閱  
 [getTime 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/gettime-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
