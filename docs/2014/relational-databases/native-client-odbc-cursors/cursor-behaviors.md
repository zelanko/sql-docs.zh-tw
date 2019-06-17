---
title: 資料指標行為 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- scrollable cursors [SQL Server]
- SQL Server Native Client ODBC driver, cursors
- version-based optimistic concurrency
- cursors [ODBC], cursor behaviors
- ODBC applications, cursors
- SQL_ATTR_CURSOR_SENSITIVITY option
- SQL_ATTR_CURSOR_SCROLLABLE option
- sensitivity behavior of cursor
- ODBC cursors, cursor behaviors
ms.assetid: 742ddcd2-232b-4aa1-9212-027df120ad35
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6c5ded9f42da267cfd137f0adfd4465d965d9a06
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188570"
---
# <a name="cursor-behaviors"></a>資料指標行為
  ODBC 透過指定資料指標的可捲動性和敏感度，支援指定其行為的 ISO 選項。 這些行為由設定 SQL_ATTR_CURSOR_SCROLLABLE 和 SQL_ATTR_CURSOR_SENSITIVITY 選項，在呼叫[SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md)。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會要求包含下列特性的伺服器資料指標，藉以實作這些選項。  
  
|資料指標行為設定|要求的伺服器資料指標特性|  
|------------------------------|---------------------------------------------|  
|SQL_SCROLLABLE 和 SQL_SENSITIVE|索引鍵集驅動資料指標和以版本為基礎的開放式並行存取|  
|SQL_SCROLLABLE 和 SQL_INSENSITIVE|靜態資料指標和唯讀並行存取|  
|SQL_SCROLLABLE 和 SQL_UNSPECIFIED|靜態資料指標和唯讀並行存取|  
|SQL_NONSCROLLABLE 和 SQL_SENSITIVE|順向資料指標和以版本為基礎的開放式並行存取|  
|SQL_NONSCROLLABLE 和 SQL_INSENSITIVE|預設結果集 (順向、唯讀)|  
|SQL_NONSCROLLABLE 和 SQL_UNSPECIFIED|預設結果集 (順向、唯讀)|  
  
 以版本為基礎的開放式並行存取需要**時間戳記**基礎資料表中的資料行。 如果沒有在資料表上要求以版本為基礎的開放式並行存取控制**時間戳記**資料行中，伺服器會使用值為基礎開放式並行存取。  
  
## <a name="scrollability"></a>可捲動性  
 當 SQL_ATTR_CURSOR_SCROLLABLE 設定為 SQL_SCROLLABLE 時，資料指標支援所有不同的值，如*Sqlfetchscroll*的參數[SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md)。 當 SQL_ATTR_CURSOR_SCROLLABLE 設定為 SQL_NONSCROLLABLE 時，資料指標僅支援*Sqlfetchscroll* SQL_FETCH_NEXT 的值。  
  
## <a name="sensitivity"></a>敏感度  
 當 SQL_ATTR_CURSOR_SENSITIVITY 設定為 SQL_SENSITIVE 時，資料指標會將目前使用者所進行或其他使用者所認可的資料修改反映出來。 當 SQL_ATTR_CURSOR_SENSITIVITY 設定為 SQL_INSENSITIVE 時，資料指標不會反映資料修改。  
  
## <a name="see-also"></a>另請參閱  
 [使用資料指標&#40;ODBC&#41;](using-cursors-odbc.md)  
  
  
