---
title: "資料指標行為 |Microsoft 文件"
ms.custom: 
ms.date: 10/24/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-cursors
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
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
caps.latest.revision: "32"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d53686929a5e6973006c812f309ddf43ea892cbf
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/24/2018
---
# <a name="cursor-behaviors"></a>資料指標行為
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC 透過指定資料指標的可捲動性和敏感度，支援指定其行為的 ISO 選項。 這些行為由設定 SQL_ATTR_CURSOR_SCROLLABLE 和 SQL_ATTR_CURSOR_SENSITIVITY 選項，在呼叫[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會要求包含下列特性的伺服器資料指標，藉以實作這些選項。  
  
|資料指標行為設定|要求的伺服器資料指標特性|  
|------------------------------|---------------------------------------------|  
|SQL_SCROLLABLE 和 SQL_SENSITIVE|索引鍵集驅動資料指標和以版本為基礎的開放式並行存取|  
|SQL_SCROLLABLE 和 SQL_INSENSITIVE|靜態資料指標和唯讀並行存取|  
|SQL_SCROLLABLE 和 SQL_UNSPECIFIED|靜態資料指標和唯讀並行存取|  
|SQL_NONSCROLLABLE 和 SQL_SENSITIVE|順向資料指標和以版本為基礎的開放式並行存取|  
|SQL_NONSCROLLABLE 和 SQL_INSENSITIVE|預設結果集 (順向、唯讀)|  
|SQL_NONSCROLLABLE 和 SQL_UNSPECIFIED|預設結果集 (順向、唯讀)|  
  
 以版本為基礎的開放式並行存取需要**時間戳記**基礎資料表中的資料行。 如果沒有在資料表上要求以版本為基礎的開放式並行存取控制，則**時間戳記**資料行中，伺服器會使用值為基礎開放式並行存取。  
  
## <a name="scrollability"></a>可捲動性  
 當 SQL_ATTR_CURSOR_SCROLLABLE 設定為 SQL_SCROLLABLE 時，資料指標支援的所有不同值*Sqlfetchscroll*參數[SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)。 當 SQL_ATTR_CURSOR_SCROLLABLE 設定為 SQL_NONSCROLLABLE 時，資料指標只支援*Sqlfetchscroll* SQL_FETCH_NEXT 的值。  
  
## <a name="sensitivity"></a>敏感度  
 當 SQL_ATTR_CURSOR_SENSITIVITY 設定為 SQL_SENSITIVE 時，資料指標會將目前使用者所進行或其他使用者所認可的資料修改反映出來。 當 SQL_ATTR_CURSOR_SENSITIVITY 設定為 SQL_INSENSITIVE 時，資料指標不會反映資料修改。  
  
## <a name="see-also"></a>另請參閱  
 [使用資料指標 (ODBC)](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md) [資料指標屬性](properties/cursor-properties.md) 
  
  
