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
ms.openlocfilehash: 997604b4376656d36d2bc4bc31f1959aa6c8a229
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67987824"
---
# <a name="ordinary-arguments"></a>一般引數
當目錄函數位符串引數為一般引數時，會將它視為常值字串。 一般引數不接受字串搜尋模式和值清單。 一般引數的大小寫很重要，且字串中的引號字元會逐字地採用。 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_FALSE，則會將這些引數視為一般引數。如果此屬性設定為 SQL_TRUE，則會將它們視為識別碼引數。  
  
 如果將一般引數設定為 null 指標，而引數是必要的引數，則此函式會傳回 SQL_ERROR 和 SQLSTATE HY009 （null 指標的用法無效）。 如果將一般引數設定為 null 指標，且引數不是必要的引數，則引數的行為會與驅動程式相關。 下表列出所需的引數。  
  
|函式|必要的引數|  
|--------------|------------------------|  
|**SQLColumnPrivileges**|*TableName*|  
|**SQLForeignKeys**|*PKTableName*、 *FKTableName*|  
|**SQLPrimaryKeys**|*TableName*|  
|**SQLSpecialColumns**|*TableName*|  
|**SQLStatistics**|*TableName*|
