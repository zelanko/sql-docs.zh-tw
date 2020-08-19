---
description: 書籤類型
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e85d50a5fe3c21707a78ac2572d8a96166745319
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476810"
---
# <a name="bookmark-types"></a>書籤類型
*ODBC 3.x 中的所有*書簽都是可變長度的書簽。 這可讓您使用與資料表相關聯的主鍵或唯一索引做為書簽。 書簽也可以是32位值， *如同 ODBC 2.x*中使用的值。 為了指定將書簽用於資料指標 *，ODBC 3.x* 應用程式會將 SQL_ATTR_USE_BOOKMARK 語句屬性設定為 SQL_UB_VARIABLE。 系統會自動使用可變長度的書簽。  
  
 應用程式可以呼叫 **SQLColAttribute** ，並將 *FieldIdentifier* 引數設定為 SQL_DESC_OCTET_LENGTH，以取得書簽的長度。 由於可變長度的書簽可以是長值，因此應用程式不應系結至資料行0，除非它會針對資料列集中的許多資料列使用書簽。  
  
 只有回溯相容性支援固定長度的書簽。 如果 ODBC 2.x*應用程式**使用 odbc 3.x*驅動程式呼叫**SQLSetStmtOption**將 SQL_USE_BOOKMARKS 設定為 SQL_UB_ON，它就會在驅動程式管理員中對應至 SQL_UB_VARIABLE。 使用可變長度的書簽，即使只填入32位的書簽。 如果驅動程式支援固定長度的書簽，則會支援可變長度的書簽。 如果 ODBC 3.x*應用程式**使用 odbc 2.x*驅動程式呼叫**SQLSetStmtAttr**將 SQL_ATTR_USE_BOOKMARKS 設定為 SQL_UB_VARIABLE，它就會在驅動程式管理員中對應到 SQL_UB_ON，並使用32位的固定長度書簽。 接著，SQL_ATTR_FETCH_BOOKMARK_PTR 語句屬性必須指向32位的書簽。 如果所使用的書簽長度超過32個位（例如，將主鍵當做書簽使用時），則資料指標必須將實際值對應至32位值。 例如，它可以建立一個雜湊表。 當*使用 odbc 2.x* *驅動程式的 odbc 3.x 應用程式*系結書簽時，緩衝區長度必須是4。
