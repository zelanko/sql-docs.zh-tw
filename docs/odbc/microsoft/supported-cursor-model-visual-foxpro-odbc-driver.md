---
title: 支援的資料指標模型 (Visual FoxPro ODBC Driver) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e623c0ce5135a4b2e558be9c405ec2757e605ceb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68080709"
---
# <a name="supported-cursor-model-visual-foxpro-odbc-driver"></a>支援的資料指標模型 (Visual FoxPro ODBC Driver)
Visual FoxPro ODBC Driver 同時支援*區塊*(*資料列集*) 和*靜態*資料指標。 靜態資料指標支援符合層級 1 ODBC 合規性的任何驅動程式。 驅動程式不支援動態、 索引鍵集驅動或混合 （索引鍵集與動態） 資料指標。  
  
 您的應用程式可以呼叫[SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) SQL_CURSOR_TYPE 選項 SQL_CURSOR_FORWARD_ONLY （區塊資料指標） 或 SQL_CURSOR_STATIC （靜態資料指標）。  
  
> [!NOTE]  
>  如果您呼叫**SQLSetStmtOption** SQL_CURSOR_FORWARD_ONLY 或 SQL_CURSOR_STATIC 以外 SQL_CURSOR_TYPE 選項，則函數會傳回 SQL_SUCCESS_WITH_INFO 的 sqlstate 01s02 的警告與 （選項值已變更）。 驅動程式會將所有不受支援的資料指標模式設定為 SQL_CURSOR_STATIC。  
  
 如需詳細資訊，關於資料指標類型和關於**SQLSetStmtOption**，請參閱[ODBC 程式設計人員參考](../../odbc/reference/odbc-programmer-s-reference.md)。  
  
## <a name="block-cursor"></a>區塊游標  
 順向捲動、 唯讀結果集，傳回給用戶端，負責維護資料的儲存體。  
  
## <a name="static-cursor"></a>靜態資料指標  
 查詢所定義的資料集的快照集。 靜態資料指標不會反映其他使用者的基礎資料的即時變更。 資料指標的記憶體緩衝區是由 ODBC 資料指標程式庫，可讓您向前及向後捲動維護。  
  
## <a name="rowset"></a>資料列集  
 資料指標，代表從資料來源擷取的資料列中儲存的資料區塊。
