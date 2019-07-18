---
title: 依書籤捲動 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
- scrolling rows [ODBC]
ms.assetid: 4862f098-41a4-4bd2-894e-f71bb97f9bc0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d27c46407e2994960af4f6abddd6cdc6f08ec852
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68055544"
---
# <a name="scrolling-by-bookmark"></a>依書籤捲動
在提取資料列時， **SQLFetchScroll**，應用程式可以使用書籤做為基礎選取起始資料列。 這是一個絕對位址的形式，因為它不相依於目前的資料指標位置。 若要捲動到加上書籤的資料列，應用程式會呼叫**SQLFetchScroll**具有*Sqlfetchscroll*要使用 sql_fetch_bookmark。 此作業使用 SQL_ATTR_FETCH_BOOKMARK_PTR 陳述式屬性所指向的書籤。 它會傳回資料列集，從該書籤識別的資料列開始。 應用程式可以指定這項作業中的位移*FetchOffset*呼叫的引數**SQLFetchScroll**。 當指定了位移時，傳回的資料列集的第一個資料列中的數字來決定*FetchOffset*的書籤所識別之資料列數目的引數。 這種使用*FetchOffset*引數不支援 ODBC 2 搭配使用時。*x*驅動程式; 當應用程式呼叫**SQLFetchScroll** ODBC 2。*x*驅動程式搭配*Sqlfetchscroll*設定為要使用 SQL_FETCH_BOOKMARK， *FetchOffset*引數必須設定為 0。
