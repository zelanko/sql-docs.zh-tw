---
description: 依書籤捲動
title: 依書簽進行滾動 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 52ef0813f3f9fd3f2d139a2549000c629943109e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476470"
---
# <a name="scrolling-by-bookmark"></a>依書籤捲動
使用 **SQLFetchScroll**提取資料列時，應用程式可以使用書簽作為選取起始列的基礎。 這是一個絕對位址的形式，因為它不相依於目前的資料指標位置。 若要滾動至有書簽的資料列，應用程式會以 SQL_FETCH_BOOKMARK 的*FetchOrientation*呼叫**SQLFetchScroll** 。 這項作業會使用 SQL_ATTR_FETCH_BOOKMARK_PTR 語句屬性所指向的書簽。 它會傳回資料列集，從該書籤識別的資料列開始。 應用程式可以在**SQLFetchScroll**呼叫的*FetchOffset*引數中，指定此作業的位移。 當指定位移時，會藉由將 *FetchOffset* 引數中的數位新增至書簽所識別的資料列數目，來決定所傳回之資料列集的第一個資料列。 搭配 ODBC 2 使用時，不支援使用*FetchOffset*引數。*x*驅動程式;當應用程式呼叫 ODBC 2 中的**SQLFetchScroll**時。將*FetchOrientation*設為 SQL_FETCH_BOOKMARK 的*x*驅動程式， *FetchOffset*引數必須設定為0。
