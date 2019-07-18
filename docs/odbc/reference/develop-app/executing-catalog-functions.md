---
title: 使用目錄函式 |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901269"
---
# <a name="executing-catalog-functions"></a>執行目錄函式
因為目錄函式會建立結果集，它就相當於執行任何結果集產生 SQL 陳述式。 事實上，目錄函數通常會實作由執行預先定義的 SQL 陳述式或呼叫預先定義的程序隨附的驅動程式或 DBMS。 幾乎適用於建立結果集的 SQL 陳述式也適用於目錄函數。 比方說，會 SQL_ATTR_MAX_ROWS 陳述式屬性限制目錄函式所傳回的資料列數目，就像它會限制傳回的資料列數目時，才**選取**陳述式。  
  
 若要執行的目錄函式，應用程式只會呼叫此函式。  
  
 如需有關目錄函數的詳細資訊，請參閱[目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。
