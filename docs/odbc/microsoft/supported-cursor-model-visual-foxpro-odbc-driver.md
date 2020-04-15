---
title: 支援的游標模型(視覺福克斯Pro ODBC驅動程式) |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301124"
---
# <a name="supported-cursor-model-visual-foxpro-odbc-driver"></a>支援的資料指標模型 (Visual FoxPro ODBC Driver)
Visual FoxPro ODBC 驅動程式支援*塊*(*行集*) 和*靜態*遊標。 任何符合 1 級 ODBC 合規性的驅動程式都支援靜態游標。 驅動程式不支援動態、鍵集驅動或混合(鍵集和動態)游標。  
  
 您的應用程式可以使用SQL_CURSOR_TYPE選項"SQL_CURSOR_FORWARD_ONLY(塊游標)或SQL_CURSOR_STATIC(靜態游標)來調用[SQLSetStmtOption。](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md)  
  
> [!NOTE]  
>  如果使用SQL_CURSOR_FORWARD_ONLY或SQL_CURSOR_STATIC以外的SQL_CURSOR_TYPE選項調用**SQLSetStmtOption,** 則函數返回SQL_SUCCESS_WITH_INFO SQLSTATE 為 01S02(選項值已更改)。 驅動程式將所有不支援的游標模式設置為SQL_CURSOR_STATIC。  
  
 有關游標類型和**SQLSetStmtOption**的詳細資訊,請參閱[ODBC 程式者的參考](../../odbc/reference/odbc-programmer-s-reference.md)。  
  
## <a name="block-cursor"></a>區塊游標  
 返回的向前滾動、只讀結果集返回給用戶端,客戶端負責維護數據的存儲。  
  
## <a name="static-cursor"></a>靜態資料指標  
 由查詢定義的數據集的快照。 靜態游標不反映其他使用者對基礎數據的即時更改。 游標的記憶體緩衝區由 ODBC 游標庫維護,允許向前和向後滾動。  
  
## <a name="rowset"></a>資料列集  
 存儲在游標中的數據塊,表示從數據源檢索的行。
