---
title: "支援資料指標模型 （Visual FoxPro ODBC 驅動程式） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], cursors
- cursors [ODBC], Visual FoxPro ODBC driver
- FoxPro ODBC driver [ODBC], cursors
- static cursors [ODBC]
- block cursors [ODBC]
- rowset cursors [ODBC]
ms.assetid: be95bbb2-6886-491e-a5a7-f58028d19c1e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b80cb7cbbea13dbc6d491d757f28d44d5fda1ea6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="supported-cursor-model-visual-foxpro-odbc-driver"></a>支援的資料指標模型 （Visual FoxPro ODBC 驅動程式）
Visual FoxPro ODBC 驅動程式同時支援*區塊*(*資料列集*) 和*靜態*資料指標。 靜態資料指標支援層級 1 ODBC 相容性符合任何驅動程式。 驅動程式不支援動態、 索引鍵集驅動或混合 （索引鍵集與動態） 資料指標。  
  
 您的應用程式可以呼叫[SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) SQL_CURSOR_FORWARD_ONLY （區塊資料指標） 或 SQL_CURSOR_STATIC （靜態資料指標） 的 SQL_CURSOR_TYPE 選項。  
  
> [!NOTE]  
>  如果您呼叫**SQLSetStmtOption** SQL_CURSOR_FORWARD_ONLY 或 SQL_CURSOR_STATIC 以外 SQL_CURSOR_TYPE 選項，此函數會傳回 SQL_SUCCESS_WITH_INFO，sqlstate 的 01s02 的警告 （選項值已變更）。 驅動程式會將所有不受支援的資料指標模式設定為 SQL_CURSOR_STATIC。  
  
 如需詳細資訊，關於資料指標類型，以及有關**SQLSetStmtOption**，請參閱[ODBC 程式設計人員參考](../../odbc/reference/odbc-programmer-s-reference.md)。  
  
## <a name="block-cursor"></a>區塊游標  
 順向捲動、 唯讀結果集傳回至用戶端負責維護資料的儲存體。  
  
## <a name="static-cursor"></a>靜態資料指標  
 查詢所定義的資料集的快照集。 靜態資料指標不會反映其他使用者對基礎資料的即時變更。 資料指標的記憶體緩衝區是由 ODBC 資料指標程式庫，可讓您向前及向後捲動維護。  
  
## <a name="rowset"></a>資料列集  
 資料指標，代表從資料來源擷取資料列中儲存的資料區塊。
