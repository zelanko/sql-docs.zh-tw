---
title: updateBytes 方法 （int，byte） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateBytes (int, byte[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 625f48ba-53d0-45a6-8fcb-643f1e0cbe8a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e61895c1d19cc2372de63be5572dcfe2d141b1fd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47831428"
---
# <a name="updatebytes-method-int-byte"></a>updateBytes 方法 (int, byte)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根據指定的資料行索引，使用 **byte** 值的陣列來更新指定的資料行。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void updateBytes(int index,  
                        byte[] x)  
```  
  
#### <a name="parameters"></a>參數  
 *index*  
  
 指出資料行索引的 **int**。  
  
 *x*  
  
 陣列**位元組**值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 UpdateBytes 方法 java.sql.ResultSet 介面中所指定這個 updateBytes 方法。  
  
 在舊版的 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 中，您可以使用 SQLServerResultSet.updateBytes 來轉換位元組陣列與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型 **date**、**time**、**datetime2** 或 **datetimeoffset** 之間的值。 現在，搭配這些資料類型使用這個方法將會引發例外狀況，指出不支援轉換。  
  
## <a name="see-also"></a>另請參閱  
 [updateBytes 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatebytes-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
