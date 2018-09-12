---
title: getObject 方法 (int) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getObject (jnt)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c4b8366b-c065-48e1-b712-19e2d9834228
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a1820a697301b9b909895faae4598d877a76ff75
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2018
ms.locfileid: "42785609"
---
# <a name="getobject-method-int"></a>getObject 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用 Java 程式語言，並配合給定的參數索引來擷取指定之參數的值當做物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.Object getObject(int index)  
```  
  
#### <a name="parameters"></a>參數  
 *index*  
  
 指出參數索引的 **int**。  
  
## <a name="return-value"></a>傳回值  
 **Object** 值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getObject 方法是由 java.sql.CallableStatement 介面中的 getObject 方法指定。  
  
 這個方法將傳回給定資料行的值來當做 Java 物件。 此 Java 物件將會是預設的 Java 物件類型，此種類型會對應到資料行的 SQL 類型，並且會對應於 JDBC 規格中所指定的內建類型。 如果該值為 SQL NULL，則驅動程式會傳回 Java null。  
  
 這個方法也可以用來讀取資料庫特性抽象資料類型。 在 JDBC 2.0 中，getObject 方法行為可進行延伸以具體化 SQL 使用者定義型別的資料。 當資料行包含結構化或相異的值時，這個方法的行為會如同呼叫 `getObject(columnIndex, this.getStatement().getConnection().getTypeMap())`。  
  
 從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 開始：  
  
-   **date** 類型的值將會以 java.sql.Date 物件形式傳回。  
  
-   **time** 類型的值將會以 java.sql.Time 物件形式傳回。  
  
-   **datetime2** 類型的值將會以 java.sql.Timestamp 物件形式傳回。  
  
-   **datetimeoffset** 類型的值將會以 microsoft.sql.DateTimeOffset 物件形式傳回。  
  
## <a name="see-also"></a>另請參閱  
 [getObject 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getobject-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
