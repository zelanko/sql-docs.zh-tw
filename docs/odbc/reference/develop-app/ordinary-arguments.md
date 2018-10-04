---
title: 一般引數 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arguments in catalog functions [ODBC], ordinary
- catalog functions [ODBC], arguments
- ordinary arguments [ODBC]
ms.assetid: a18cdae1-6b85-41cb-875c-b5a01ec90aeb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 31d83b00fd70cd54587a19ebfea7310154167493
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47706683"
---
# <a name="ordinary-arguments"></a>一般引數
目錄函式的字串引數時的一般引數，則會視為常值的字串。 字串搜尋模式和一份值都不會接受一般引數。 一般的引數的案例是有意義的並在字串中的引號字元會解譯為常值。 這些引數會被視為一般引數如果 SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_FALSE。它們會被視為識別碼引數而如果此屬性設定為 SQL_TRUE。  
  
 如果一般引數設定為 null 指標引數是必要的引數，則函數會傳回 SQL_ERROR，而且 SQLSTATE HY009 （使用無效的 null 指標）。 如果一般引數設定為 null 指標引數不是必要的引數，引數的行為會與驅動程式相關。 下表詳列的必要引數。  
  
|函數|必要的引數|  
|--------------|------------------------|  
|**SQLColumnPrivileges**|*TableName*|  
|**SQLForeignKeys**|*PKTableName*， *FKTableName*|  
|**SQLPrimaryKeys**|*TableName*|  
|**SQLSpecialColumns**|*TableName*|  
|**SQLStatistics**|*TableName*|
