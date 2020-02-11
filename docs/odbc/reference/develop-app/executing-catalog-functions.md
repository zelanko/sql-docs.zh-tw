---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ab6eba9c4a3df3e16e35d8a93dc95209a093fb80
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67901269"
---
# <a name="executing-catalog-functions"></a>執行目錄函式
因為目錄函數會建立結果集，所以它相當於執行任何結果集產生的 SQL 語句。 事實上，目錄函數通常是透過執行預先定義的 SQL 語句或呼叫驅動程式或 DBMS 隨附的預先定義程式來執行。 幾乎所有適用于建立結果集之 SQL 語句的專案也適用于目錄函數。 例如，SQL_ATTR_MAX_ROWS 語句屬性會限制目錄函數所傳回的資料列數目，就像它會限制**SELECT**語句所傳回的資料列數一樣。  
  
 若要執行目錄函式，應用程式只會呼叫函數。  
  
 如需目錄函式的詳細資訊，請參閱[目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。
