---
title: "execute 方法 (java.lang.String，int[]) |Microsoft 文件"
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
- SQLServerStatement.execute (javal.lang.String.int[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: dc73d1c3-e756-43af-b1fc-ac438cbd0965
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 50cb9686b883ac0a4d682e7ea28f1dba40257c7e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="execute-method-javalangstring-int"></a>execute 方法 (java.lang.String, int[])

  執行給定的 SQL 陳述式，可傳回多個結果，以及訊號[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion-md.md)]給定陣列中所指出的自動產生索引鍵應該進行擷取。

## <a name="syntax"></a>語法

```Java
public final boolean execute(
    java.lang.String sql,
    int[] columnIndexes)
```

#### <a name="parameters"></a>參數
*sql*

A**字串**，其中包含 SQL 陳述式。

*columnIndexes*

陣列**int**，指出應該提供的自動產生索引鍵的資料行索引。

## <a name="return-value"></a>傳回值
**true**如果第一個結果是結果集。 否則為 **false**。
  
## <a name="exceptions"></a>例外狀況
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>備註
這個 execute 方法是由 java.sql.Statement 介面中的 execute 方法中指定。

## <a name="see-also"></a>另請參閱

[執行方法 &#40;SQLServerStatement &#41;](./execute-method-sqlserverstatement.md)

[SQLServerStatement 成員](./sqlserverstatement-members.md)

[SQLServerStatement 類別](./sqlserverstatement-class.md)

