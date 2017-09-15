---
title: "executeUpdate 方法 (java.lang.String) |Microsoft 文件"
ms.custom: 
ms.date: 02/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerPreparedStatement.executeUpdate (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 91ecb1cd-001d-4ac9-9ae8-5db05c3c2959
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 264ccb901e544eb0990f39ed53d112c7f8e9220f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="executeupdate-method-javalangstring"></a>executeUpdate 方法 (java.lang.String)

執行可能是 INSERT、UPDATE、MERGE 或 DELETE 陳述式的給定 SQL 陳述式，否則會是不傳回任何項目的 SQL 陳述式，例如 SQL DDL 陳述式。

## <a name="syntax"></a>語法

```
public final int executeUpdate(java.lang.String sql)
```

#### <a name="parameters"></a>參數
*sql*

A**字串**，其中包含 SQL 陳述式。

## <a name="return-value"></a>傳回值
**Int** ，指出資料列受到影響或 0 的數目，如果使用 DDL 陳述式。

## <a name="exceptions"></a>例外狀況
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>備註
這個 executeUpdate 方法是由 java.sql.PreparedStatement 介面中的 executeUpdate 方法指定。

呼叫這個方法會導致例外狀況，因為在建立物件時指定 SQLServerPreparedStatement 物件的 SQL 陳述式。

## <a name="see-also"></a>另請參閱

[executeUpdate 方法 &#40;SQLServerPreparedStatement &#41;](./executeupdate-method-sqlserverpreparedstatement.md)

[SQLServerPreparedStatement 成員](./sqlserverpreparedstatement-members.md)

[SQLServerPreparedStatement 類別](./sqlserverpreparedstatement-class.md)

