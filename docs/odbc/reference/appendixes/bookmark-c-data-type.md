---
description: 書籤 C 資料類型
title: 書簽 C 資料類型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- C data types [ODBC], bookmark C data type
- pseudo-type identifiers [ODBC], bookmark C data type
- data types [ODBC], pseudo-type identifiers
- bookmarks [ODBC]
- bookmark C data type [ODBC]
ms.assetid: add88e48-ada3-4c0c-a5ac-e78903d3ff41
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4647002d5e57ea20656a4fa2dec03aa8092b9b36
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411254"
---
# <a name="bookmark-c-data-type"></a>書籤 C 資料類型
書簽 C 資料類型可讓應用程式取出書簽。 書簽 C 類型只能用來取出可作為變數長度的書簽值;它們不應轉換成其他資料類型。 應用程式會從結果集的資料行0（具有 **SQLBulkOperations** (，並將 SQL_ADD) 、 **SQLFetch**、 **SQLFetchScroll**或 **SQLGetData**）抓取書簽。 如需詳細資訊，請參閱 [書簽](../../../odbc/reference/develop-app/bookmarks-odbc.md)。  
  
 下表列出「書簽 C」資料類型的 *CType* 值、實作為「書簽 c」資料類型的 ODBC c 資料類型，以及此資料類型在 SQL 中的定義。H。  
  
> [!NOTE]
>  SQL_C_BOOKMARK 的資料類型已被取代。 ODBC *3.x* 應用程式不應該使用 SQL_C_BOOKMARK。 只有當 ODBC 3.x 驅動程式想要搭配*使用 odbc 2.x*應用程式時，才需要支援*SQL_C_BOOKMARK。* 當應用程式 *與 ODBC 2.x 驅動程式搭配* 使用時，驅動程式管理員會將 SQL_C_VARBOOKMARK 對應到 SQL_C_BOOKMARK。  
  
|C 類型識別碼|ODBC C typedef|C 類型|  
|-----------------------|--------------------|------------|  
|SQL_C_BOOKMARK<br />(已被取代)|書簽|unsigned long int|  
|SQL_C_VARBOOKMARK|SQLCHAR|unsigned char *|
