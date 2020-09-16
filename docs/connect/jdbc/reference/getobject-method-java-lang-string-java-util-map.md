---
description: getObject 方法 (java.lang.String, java.util.Map)
title: getObject 方法 (java.lang.String, java.util.Map) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getObject (java.lang.String, Java.util.Map)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e174eb81-d569-479e-a171-365cd6d44b6a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 58b1857781baea98e3dca98c00a69b20284a3235
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88435120"
---
# <a name="getobject-method-javalangstring-javautilmap"></a>getObject 方法 (java.lang.String, java.util.Map)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用 Java 程式設計語言以指定的參數名稱，透過指定的 Map 物件，擷取指定的參數值作為物件。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 目前不支援這個方法。 因此，使用這個方法時一定會傳回預設對應。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.Object getObject(java.lang.String sCol,  
                                  java.util.Map m)  
```  
  
#### <a name="parameters"></a>參數  
 *sCol*  
  
 包含參數名稱的**字串**。  
  
 *m*  
  
 Map 物件。  
  
## <a name="return-value"></a>傳回值  
 **Object** 值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getObject 方法是由 java.sql.CallableStatement 介面中的 getObject 方法指定。  
  
 這個方法將傳回給定資料行的值來當做 Java 物件。 此 Java 物件將會是預設的 Java 物件類型，此種類型會對應到資料行的 SQL 類型，並且會對應於 JDBC 規格中所指定的內建類型。 如果該值為 SQL NULL，則驅動程式會傳回 Java null。  
  
 這個方法也可以用來讀取資料庫特性抽象資料類型。 在 JDBC 2.0 API 中，會延伸 getObject 方法的行為，以具體化 SQL 使用者定義型別的資料。 當資料行包含結構化或相異的值，這個方法的行為會如同對 `getObject(columnIndex, this.getStatement().getConnection().getTypeMap())` 的呼叫。  
  
 從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC 驅動程式 3.0 開始：  
  
-   **date** 類型的值將會以 java.sql.Date 物件的形式傳回。  
  
-   **time** 類型的值將會以 java.sql.Time 物件的形式傳回。  
  
-   **datetime2** 類型的值將會以 java.sql.Timestamp 物件的形式傳回。  
  
-   **datetimeoffset** 類型的值將會以 microsoft.sql.DateTimeOffset 物件形式傳回。  
  
## <a name="see-also"></a>另請參閱  
 [getObject 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getobject-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
