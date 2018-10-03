---
title: getBytes 方法 (int) (SQLServerResultSet) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getBytes (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1385d7d4-9288-4cbd-8606-4b919e9b07b2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 631534e2ca1d0fe7a4c127acb277fc9db7208ace
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47722286"
---
# <a name="getbytes-method-int-sqlserverresultset"></a>getBytes 方法 (int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用 Java 程式設計語言，從這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件目前資料列中擷取指定的資料行索引值來當作 **byte** 陣列。  
  
## <a name="syntax"></a>語法  
  
```  
  
public byte[] getBytes(int columnIndex)  
```  
  
#### <a name="parameters"></a>參數  
 *columnIndex*  
  
 指出資料行索引的 **int**。  
  
## <a name="return-value"></a>傳回值  
 陣列**位元組**值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getBytes 方法是由 java.sql.ResultSet 介面中的 getBytes 方法指定。  
  
 這個方法支援從伺服器擷取所有資料行當做原始的位元組讀取。 它會直接從伺服器傳回位元組的陣列 (使用儲存於伺服器上的格式)。  
  
 在舊版的 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 中，您可以使用 SQLServerResultSet.getBytes 來轉換位元組陣列與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型 **date**、**time**、**datetime2** 或 **datetimeoffset** 之間的值。 現在，搭配這些資料類型使用這個方法將會引發例外狀況，指出不支援轉換。  
  
## <a name="see-also"></a>另請參閱  
 [getBytes 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getbytes-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
