---
description: 一般引數
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b6e4e7a30efe5735aa87665d7d0247bef06390ce
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429170"
---
# <a name="ordinary-arguments"></a>一般引數
當目錄函數位符串引數是一般的引數時，它會被視為常值字串。 一般引數不接受字串搜尋模式，也不接受值的清單。 一般引數的大小寫很重要，而字串中的引號字元會以文字形式取得。 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_FALSE，則會將這些引數視為一般引數。如果這個屬性設定為 SQL_TRUE，則會將它們視為識別碼引數。  
  
 如果將一般引數設定為 null 指標，且引數是必要的引數，則函式會傳回 SQL_ERROR 和 SQLSTATE HY009 (不正確 null 指標) 用法。 如果一般引數設定為 null 指標，且引數不是必要的引數，則引數的行為取決於驅動程式。 下表列出必要的引數。  
  
|函式|必要的引數|  
|--------------|------------------------|  
|**SQLColumnPrivileges**|*名*|  
|**SQLForeignKeys**|*PKTableName*、 *FKTableName*|  
|**SQLPrimaryKeys**|*名*|  
|**SQLSpecialColumns**|*名*|  
|**SQLStatistics**|*名*|
