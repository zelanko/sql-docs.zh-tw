---
title: 描述項欄位的初始化 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- initializing descriptor fields [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 1da157cb-8ea9-4a56-983b-1c45650217c5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d988099cad357254f04a79a8a6cccbbe4eb2768c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62446809"
---
# <a name="initialization-of-descriptor-fields"></a>描述項欄位的初始設定
當配置的應用程式資料列描述項時，其欄位中所示收到初始值[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。 SQL_DESC_TYPE 欄位的初始值是 SQL_DEFAULT。 這會提供標準的處理方式，來呈現給應用程式的資料庫資料。 應用程式可以藉由設定描述項記錄的欄位指定資料的處理方式不同。  
  
 描述項標頭中的 SQL_DESC_ARRAY_SIZE 初始值為 1。 應用程式可以修改此欄位，可讓多資料列擷取。  
  
 預設值的概念的 IRD 欄位無效。 應用程式可以存取的 IRD 欄位時，才與它相關聯的已備妥或已執行的陳述式。  
  
 只有在 IPD 自動填入驅動程式之後，才定義 IPD 的特定欄位。 如果沒有，也就是未定義。 這些欄位是 SQL_DESC_CASE_SENSITIVE、 SQL_DESC_FIXED_PREC_SCALE、 SQL_DESC_TYPE_NAME、 SQL_DESC_UNSIGNED 和 SQL_DESC_LOCAL_TYPE_NAME。
