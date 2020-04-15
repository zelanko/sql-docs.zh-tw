---
title: 書籤 C 資料類型 |微軟文件
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
ms.openlocfilehash: 566f1065d30a47b2db234ba1f11f877725189fb7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292288"
---
# <a name="bookmark-c-data-type"></a>書籤 C 資料類型
書籤 C 數據類型允許應用程式檢索書籤。 書籤 C 類型僅用於檢索長度可可變的書籤值;它們不應轉換為其他數據類型。 應用程式**從結果集**的第 0 列檢索書籤(操作為 SQL_ADD)、SQLFetch、SQLFetchScroll 或**SQLFetch** **SQLFetchScroll** **SQLGetData**。 有關詳細資訊,請參閱[書籤](../../../odbc/reference/develop-app/bookmarks-odbc.md)。  
  
 下表列出了書籤 C 資料類型的*CType*值、實現書籤 C 數據類型的 ODBC C 數據類型以及 SQL 中此數據類型的定義。H。  
  
> [!NOTE]
>  已棄用SQL_C_BOOKMARK數據類型。 ODBC *3.x*應用程式不應使用SQL_C_BOOKMARK。 ODBC *3.x*驅動程式只有在希望使用 ODBC *2.x*應用程式時才需要支援SQL_C_BOOKMARK。 當應用程式使用 ODBC *2.x*驅動程式工作時,驅動程式管理器將SQL_C_VARBOOKMARK映射到SQL_C_BOOKMARK。  
  
|C 類型識別碼|ODBC C 型定義|C 類型|  
|-----------------------|--------------------|------------|  
|SQL_C_BOOKMARK<br />(已被取代)|書籤|unsigned long int|  
|SQL_C_VARBOOKMARK|SQLCHAR ||unsigned char *|
