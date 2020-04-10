---
title: getNClob 方法 (int) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 103082e3-de98-4dff-8dc7-eaa5c64b1597
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 05579be0147a7a5349008be1f014bf3dbb1f2ebf
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80905724"
---
# <a name="getnclob-method-int-sqlserverresultset"></a>getNClob 方法 (int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用 Java 程式設計語言，擷取 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件目前資料列中所指定資料行的值來作為 NClob 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.NClob getNClob(int columnIndex)  
```  
  
#### <a name="parameters"></a>參數  
 *columnIndex*  
  
 指出資料行索引的 **int**。  
  
## <a name="return-value"></a>傳回值  
 NClob 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getNClob 方法是由 java.sql.ResultSet 介面中的 getNClob 方法指定。  
  
 只有在 **nvarchar(max)** 、**ntext** 和 **xml** 資料行上才支援這個方法。 對任何其他資料類型使用這個方法，將擲回例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [getNClob 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getnclob-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
