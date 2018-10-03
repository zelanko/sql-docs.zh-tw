---
title: getDateTimeOffset(int) (SQLServerResultSet) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 60abf83d-6f97-4e47-b9d3-5072bd09d869
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1ab888a8845f5cd718837d6a534e36bd83950da1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47623966"
---
# <a name="getdatetimeoffsetint-sqlserverresultset"></a>getDateTimeOffset(int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  這個方法是在 [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 中所新增。  
  
 使用 Java 程式設計語言，並配合所指定參數索引來擷取指定資料行值當作 [DateTimeOffset 類別](../../../connect/jdbc/reference/datetimeoffset-class.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public microsoft.sql.DateTimeOffset getDateTimeOffset(int columnIndex)  
```  
  
#### <a name="parameters"></a>參數  
 *columnIndex*  
  
 資料行序數。  
  
## <a name="return-value"></a>傳回值  
 A [DateTimeOffset 類別](../../../connect/jdbc/reference/datetimeoffset-class.md)物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 您可以更新[DateTimeOffset 類別](../../../connect/jdbc/reference/datetimeoffset-class.md)值替換[sqlserverresultset.updatedatetimeoffset 來](../../../connect/jdbc/reference/updatedatetimeoffset-sqlserverresultset.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
