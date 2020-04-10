---
title: execute 方法 (java.lang.String, int[]) | Microsoft Docs
ms.custom: ''
ms.date: 02/07/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.execute (javal.lang.String.int[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: dc73d1c3-e756-43af-b1fc-ac438cbd0965
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7195d5c5bf4efb593e53dea6e5404cc8adb70830
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922122"
---
# <a name="execute-method-javalangstring-int"></a>execute 方法 (java.lang.String, int[])

  執行可傳回多個結果的指定 SQL 陳述式，並向 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 發出訊號，通知必須提供指定陣列所指出的自動產生索引鍵以進行擷取。

## <a name="syntax"></a>語法

```Java
public final boolean execute(
    java.lang.String sql,
    int[] columnIndexes)
```

#### <a name="parameters"></a>參數
*sql*

包含 SQL 陳述式的**字串**。

*columnIndexes*

**int** 的陣列，這些值指出必須提供自動產生索引鍵的資料行索引。

## <a name="return-value"></a>傳回值
如果第一個結果是結果集，則為 **true** 否則為 **false**。
  
## <a name="exceptions"></a>例外狀況
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>備註
這個 execute 方法是由 java.sql.Statement 介面中的 execute 方法指定。

## <a name="see-also"></a>另請參閱

[execute 方法 &#40;SQLServerStatement&#41;](./execute-method-sqlserverstatement.md)

[SQLServerStatement 成員](./sqlserverstatement-members.md)

[SQLServerStatement 類別](./sqlserverstatement-class.md)
