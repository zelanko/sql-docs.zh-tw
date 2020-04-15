---
title: 執行目錄函數 :微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], executing
- functions [ODBC], catalog functions
ms.assetid: c59cbda3-e214-4399-9edc-cfac86b378d7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6469a5394e232ab9d9135fbbbd56ba7b791ccbcb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305719"
---
# <a name="executing-catalog-functions"></a>執行目錄函式
由於目錄函數創建結果集,因此等效於執行任何結果集生成的 SQL 語句。 事實上,目錄函數通常是通過執行預定義的 SQL 語句或調用驅動程式或 DBMS 附帶的預定義過程實現的。 幾乎所有適用於創建結果集的 SQL 語句都適用於目錄函數。 例如,SQL_ATTR_MAX_ROWS語句屬性限制目錄函數返回的行數,就像它限制**SELECT**語句返回的行數一樣。  
  
 要執行目錄函數,應用程式只需調用該函數。  
  
 有關目錄函數的詳細資訊,請參閱[目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。
