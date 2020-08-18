---
description: 執行目錄函式
title: 執行目錄函數 |Microsoft Docs
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
ms.openlocfilehash: 19baae1518078c44b8e170fb623eab0087bac12a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482911"
---
# <a name="executing-catalog-functions"></a>執行目錄函式
因為目錄函數會建立結果集，所以它相當於執行任何結果集產生的 SQL 語句。 事實上，類別目錄函式通常是藉由執行預先定義的 SQL 語句，或呼叫隨附于驅動程式或 DBMS 的預先定義程式來執行。 幾乎適用于建立結果集之 SQL 語句的任何內容，也適用于目錄函數。 例如，SQL_ATTR_MAX_ROWS 語句屬性會限制 catalog 函數所傳回的資料列數目，就像它會限制 **SELECT** 語句所傳回的資料列數目一樣。  
  
 若要執行目錄函數，應用程式只會呼叫函數。  
  
 如需目錄函式的詳細資訊，請參閱 [類別目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。
