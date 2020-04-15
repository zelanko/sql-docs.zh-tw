---
title: 普通參數 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 97362f93e91ccd8b592b4c05a0714b7602c1ba94
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282460"
---
# <a name="ordinary-arguments"></a>一般引數
當目錄函數位串參數是普通參數時,它被視為文本字串。 普通參數既不接受字串搜索模式,也不接受值清單。 普通參數的情況很重要,字串中的報價字元是字面上的。 如果SQL_ATTR_METADATA_ID語句屬性設置為SQL_FALSE,則這些參數將被視為普通參數。如果此屬性設置為SQL_TRUE,則它們將被視為標識符參數。  
  
 如果普通參數設置為空指標,並且參數是必需的參數,則函數將返回SQL_ERROR和 SQLSTATE HY009(無效使用空指標)。 如果普通參數設置為空指標,並且該參數不是必需的參數,則該參數的行為取決於驅動程式。 下表列出了所需的參數。  
  
|函式|必要參數|  
|--------------|------------------------|  
|**SQLColumnPrivileges**|*表格名稱*|  
|**SQLForeignKeys**|*PKTable 名稱*, *FKTable 名稱*|  
|**SQLPrimaryKeys**|*表格名稱*|  
|**SQLSpecialColumns**|*表格名稱*|  
|**SQLStatistics**|*表格名稱*|
