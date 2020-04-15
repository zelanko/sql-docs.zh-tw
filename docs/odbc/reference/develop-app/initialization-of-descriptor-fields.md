---
title: 描述符欄位的初始化 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e4ed6479a60f1d0695107c216b2f0c94a55f68ff
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300118"
---
# <a name="initialization-of-descriptor-fields"></a>描述項欄位的初始設定
分配應用程式行描述符時,其欄位將接收[SQLSetDescField 中](../../../odbc/reference/syntax/sqlsetdescfield-function.md)指示的初始值。 SQL_DEFAULTSQL_DESC_TYPE欄位的初始值。 這提供了資料庫數據的標準處理,以便向應用程式演示。 應用程式可以通過設置描述符記錄的欄位來指定對數據的不同處理。  
  
 描述符標頭中SQL_DESC_ARRAY_SIZE的初始值為 1。 應用程式可以修改此欄位以啟用多行提取。  
  
 預設值的概念對 IRD 的欄位無效。 僅當存在與其關聯的已準備或執行語句時,應用程式才能訪問 IRD 的欄位。  
  
 IPD 的某些欄位僅在驅動程式自動填充 IPD 後定義。 如果沒有,它們未定義。 這些字段SQL_DESC_CASE_SENSITIVE、SQL_DESC_FIXED_PREC_SCALE、SQL_DESC_TYPE_NAME、SQL_DESC_UNSIGNED 和SQL_DESC_LOCAL_TYPE_NAME。
