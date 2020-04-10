---
title: prepareStatement 方法 (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 02/07/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.prepareStatement (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e825765c-eb55-4800-951b-f3495da36641
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4b17c514a293f4566c3408e364acccbab721e1ce
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923133"
---
# <a name="preparestatement-method-javalangstring"></a>prepareStatement 方法 (java.lang.String)

建立 [SQLServerPreparedStatement](./sqlserverpreparedstatement-class.md) 物件，以便將參數化 SQL 陳述式傳送至資料庫。

## <a name="syntax"></a>語法

```
public java.sql.PreparedStatement prepareStatement(java.lang.String sql)
```

#### <a name="parameters"></a>參數
*sql*

**String**，其中包含 SQL 陳述式。

## <a name="return-value"></a>傳回值
PreparedStatement 物件。

## <a name="exceptions"></a>例外狀況  
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>備註
這個 prepareStatement 方法是由 java.sql.Connection 介面中的 prepareStatement 方法所指定。

## <a name="see-also"></a>另請參閱

[prepareStatement 方法 &#40;SQLServerConnection&#41;](./preparestatement-method-sqlserverconnection.md)

[SQLServerConnection 成員](./sqlserverconnection-members.md)

[SQLServerConnection 類別](./sqlserverconnection-class.md)
