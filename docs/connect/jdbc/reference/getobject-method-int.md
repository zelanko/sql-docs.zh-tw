---
title: "getObject 方法 (int) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerCallableStatement.getObject (jnt)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c4b8366b-c065-48e1-b712-19e2d9834228
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4e43c9e04aefe5b0c658ab41112cfdf764454291
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getobject-method-int"></a>getObject 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用 Java 程式語言，並配合給定的參數索引來擷取指定之參數的值當做物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.Object getObject(int index)  
```  
  
#### <a name="parameters"></a>參數  
 *索引*  
  
 **Int** ，指出參數索引。  
  
## <a name="return-value"></a>傳回值  
 **物件**值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getObject 方法是由 java.sql.CallableStatement 介面中的 getObject 方法指定。  
  
 這個方法將傳回給定資料行的值來當做 Java 物件。 此 Java 物件將會是預設的 Java 物件類型，此種類型會對應到資料行的 SQL 類型，並且會對應於 JDBC 規格中所指定的內建類型。 如果該值為 SQL NULL，則驅動程式會傳回 Java null。  
  
 這個方法也可以用來讀取資料庫特性抽象資料類型。 在 JDBC 2.0 getObject 方法的行為已延伸以具體化 SQL 使用者定義類型的資料。 當資料行包含的結構化或相異值時，就如同呼叫這個方法的行為`getObject(columnIndex, this.getStatement().getConnection().getTypeMap())`。  
  
 從開始[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]JDBC 驅動程式 3.0:  
  
-   型別的值**日期**將傳回來當做 java.sql.Date 物件。  
  
-   型別的值**時間**將傳回來當做 java.sql.Time 物件。  
  
-   型別的值**datetime2**將傳回來當做 java.sql.Timestamp 物件。  
  
-   型別的值**datetimeoffset**將會以 microsoft.sql.DateTimeOffset 物件的形式傳回。  
  
## <a name="see-also"></a>另請參閱  
 [getObject 方法 &#40;SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getobject-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

