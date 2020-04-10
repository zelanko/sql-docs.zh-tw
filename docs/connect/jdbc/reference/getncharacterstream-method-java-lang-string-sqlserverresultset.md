---
title: getNCharacterStream 方法 (java.lang.String) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a117f3a3-9c25-41e1-9adb-a40e90620dd6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6b4354f104564e8aff2aceb08758b0405005134a
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80905887"
---
# <a name="getncharacterstream-method-javalangstring-sqlserverresultset"></a>getNCharacterStream 方法 (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列中所指定資料行的值來當作 Reader 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.io.Reader getNCharacterStream(java.lang.String columnLabel)  
```  
  
#### <a name="parameters"></a>參數  
 *columnLabel*  
  
 String，包含資料行標籤。  
  
## <a name="return-value"></a>傳回值  
 Reader 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getNCharacterStream 方法是由 java.sql.ResultSet 介面中的 getNCharacterStream 方法所指定。  
  
 這個方法可以用來擷取這個 **SQLServerResultSet** 物件目前資料列中 **nvarchar**、**nchar**、**nvarchar(max)** 、**ntext** 或 [xml](../../../connect/jdbc/reference/sqlserverresultset-class.md) 資料行的值。 如果嘗試使用這個方法來擷取其他資料類型的值，將擲回例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [getNCharacterStream 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getncharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)  
  
  
