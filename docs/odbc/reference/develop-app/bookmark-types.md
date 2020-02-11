---
title: 書簽類型 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fb8f5848ef9fdffab8592215fdcc5406b24319c3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68118776"
---
# <a name="bookmark-types"></a>書籤類型
*ODBC 3.x 中的所有*書簽都是可變長度的書簽。 這可讓與資料表相關聯的主鍵或唯一索引當做書簽使用。 書簽也可以是32位的值，就像在 ODBC 2.x 中使用*一樣。* 若要指定將書簽用於資料指標 *，ODBC 3.x*應用程式會將 SQL_ATTR_USE_BOOKMARK 語句屬性設定為 SQL_UB_VARIABLE。 系統會自動使用可變長度的書簽。  
  
 應用程式可以呼叫**SQLColAttribute** ，並將*FieldIdentifier*引數設為 SQL_DESC_OCTET_LENGTH 以取得書簽的長度。 由於可變長度的書簽可以是 long 值，因此除非應用程式將會針對資料列集中的許多資料列使用書簽，否則不應系結至資料行0。  
  
 固定長度的書簽僅支援回溯相容性。 如果*使用 odbc 3.x* *驅動程式的 odbc 2.x 應用程式*呼叫**SQLSetStmtOption** ，將 SQL_USE_BOOKMARKS 設定為 SQL_UB_ON，則會在驅動程式管理員中將它對應至 SQL_UB_VARIABLE。 使用可變長度的書簽，即使只填入32位也一樣。 如果驅動程式支援固定長度的書簽，則會支援可變長度的書簽。 如果*使用 odbc 2.x* *驅動程式的 odbc 3.x 應用程式*呼叫**SQLSetStmtAttr** ，將 SQL_ATTR_USE_BOOKMARKS 設定為 SQL_UB_VARIABLE，則會在驅動程式管理員中將它對應到 SQL_UB_ON，並使用32位的固定長度書簽。 SQL_ATTR_FETCH_BOOKMARK_PTR 語句屬性必須指向32位的書簽。 如果所使用的書簽長度超過32位（例如將主鍵當做書簽使用時），則游標必須將實際的值對應至32位的值。 例如，它可以建立雜湊表。 使用 ODBC 2.x*驅動程式來*系結書簽時， ** 緩衝區長度必須為4。
