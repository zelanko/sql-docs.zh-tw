---
title: 支援的資料指標模型（Visual FoxPro ODBC Driver） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], cursors
- cursors [ODBC], Visual FoxPro ODBC driver
- FoxPro ODBC driver [ODBC], cursors
- static cursors [ODBC]
- block cursors [ODBC]
- rowset cursors [ODBC]
ms.assetid: be95bbb2-6886-491e-a5a7-f58028d19c1e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cf3400f24e20a8fa864404612bf07ea44efce49e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301124"
---
# <a name="supported-cursor-model-visual-foxpro-odbc-driver"></a>支援的資料指標模型 (Visual FoxPro ODBC Driver)
Visual FoxPro ODBC 驅動程式同時支援*區塊（資料列**集*）和*靜態*資料指標。 符合 Level 1 ODBC 合規性的任何驅動程式都支援靜態資料指標。 驅動程式不支援動態、索引鍵集驅動或混合（索引鍵集和動態）資料指標。  
  
 您的應用程式可以使用 SQL_CURSOR_FORWARD_ONLY 的 SQL_CURSOR_TYPE 選項（區塊游標）或 SQL_CURSOR_STATIC （靜態資料指標）來呼叫[SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) 。  
  
> [!NOTE]  
>  如果您使用 SQL_CURSOR_FORWARD_ONLY 或 SQL_CURSOR_STATIC 以外的 SQL_CURSOR_TYPE 選項來呼叫**SQLSetStmtOption** ，此函式會傳回 SQL_SUCCESS_WITH_INFO，SQLSTATE 為01S02 （選項值已變更）。 驅動程式會將所有不支援的資料指標模式設定為 SQL_CURSOR_STATIC。  
  
 如需資料指標類型和有關**SQLSetStmtOption**的詳細資訊，請參閱 ODBC 程式設計[人員參考](../../odbc/reference/odbc-programmer-s-reference.md)。  
  
## <a name="block-cursor"></a>區塊游標  
 向用戶端傳回的順向滾動唯讀結果集，負責維護資料的儲存體。  
  
## <a name="static-cursor"></a>靜態資料指標  
 查詢所定義之資料集的快照集。 靜態資料指標不會反映其他使用者對基礎資料的即時變更。 資料指標的記憶體緩衝區是由 ODBC 資料指標程式庫所維護，可允許向前和向後滾動。  
  
## <a name="rowset"></a>資料列集  
 儲存在資料指標中的資料區塊，代表從資料來源抓取的資料列。
