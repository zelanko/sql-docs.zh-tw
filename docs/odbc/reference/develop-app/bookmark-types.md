---
title: 書籤類型 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- variable-length bookmarks [ODBC]
- bookmarks [ODBC]
- fixed-length bookmarks [ODBC]
ms.assetid: cb2e7443-0260-4d1a-930f-0154db447979
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 26d0297cd9dc57e9f30945a9248b235ae469da3e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306329"
---
# <a name="bookmark-types"></a>書籤類型
ODBC *3.x*中的所有書籤都是可變長度的書籤。 這允許將主鍵或與表關聯的唯一索引用作書籤。 書籤也可以是 32 位值,如 ODBC *2.x*中使用的那樣。 要指定書籤與游標一起使用,ODBC *3.x*應用程式將SQL_ATTR_USE_BOOKMARK語句屬性設置為SQL_UB_VARIABLE。 將自動使用可變長度書籤。  
  
 應用程式可以調用**SQLColAttribute,** 欄位*識別符*參數設置為SQL_DESC_OCTET_LENGTH以獲取書籤的長度。 由於可變長度書籤可以是長值,因此應用程式不應綁定到列 0,除非它將對行集中的許多行使用書籤。  
  
 固定長度書簽僅支援向後相容性。 如果使用 ODBC *3.x*驅動程式的 ODBC *2.x*應用程式呼叫**SQLSetStmtOption**將SQL_USE_BOOKMARKS設定為SQL_UB_ON,則它將在驅動程式管理器中對應到SQL_UB_VARIABLE。 使用可變長度書籤,即使只填充了 32 位書籤。 如果驅動程式支援固定長度書籤,它將支援可變長度書籤。 如果使用 ODBC *2.x*驅動程式的 ODBC *3.x*應用程式呼叫**SQLSetStmtAttr**將SQL_ATTR_USE_BOOKMARKS設定為SQL_UB_VARIABLE,則它將在驅動程式管理器中映射到SQL_UB_ON,並且使用 32 位元固定長度書籤。 然後,SQL_ATTR_FETCH_BOOKMARK_PTR語句屬性必須指向 32 位書籤。 如果使用的書籤長於 32 位元(例如,當主鍵用作書籤時)時,游標必須將實際值映射到 32 位值。 例如,它可以構建它們的哈希表。 當使用 ODBC *2.x*驅動程式的 ODBC *3.x*應用程式綁定書籤時,緩衝區長度必須為 4。
