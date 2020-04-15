---
title: 游標行為 |微軟文件
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f2e3400e52cd0b7574c07a3cf813b4cbca317df2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305456"
---
# <a name="cursor-behaviors"></a>資料指標行為
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC 透過指定資料指標的可捲動性和敏感度，支援指定其行為的 ISO 選項。 這些行為是通過在調用[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)時設置SQL_ATTR_CURSOR_SCROLLABLE和SQL_ATTR_CURSOR_SENSITIVITY選項來指定的。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會要求包含下列特性的伺服器資料指標，藉以實作這些選項。  
  
|資料指標行為設定|要求的伺服器資料指標特性|  
|------------------------------|---------------------------------------------|  
|SQL_SCROLLABLE 和 SQL_SENSITIVE|索引鍵集驅動資料指標和以版本為基礎的開放式並行存取|  
|SQL_SCROLLABLE 和 SQL_INSENSITIVE|靜態資料指標和唯讀並行存取|  
|SQL_SCROLLABLE 和 SQL_UNSPECIFIED|靜態資料指標和唯讀並行存取|  
|SQL_NONSCROLLABLE 和 SQL_SENSITIVE|順向資料指標和以版本為基礎的開放式並行存取|  
|SQL_NONSCROLLABLE 和 SQL_INSENSITIVE|預設結果集 (順向、唯讀)|  
|SQL_NONSCROLLABLE 和 SQL_UNSPECIFIED|預設結果集 (順向、唯讀)|  
  
 基於版本的樂觀併發需要基礎表中**的時間戳**列。 如果在沒有**時間戳**列的表上請求基於版本的樂觀併發控制,則伺服器將使用基於值的樂觀併發。  
  
## <a name="scrollability"></a>可捲動性  
 當SQL_ATTR_CURSOR_SCROLLABLE設置為SQL_SCROLLABLE時,游標支援[SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)的*Fetch 方向*參數的所有不同值。 當SQL_ATTR_CURSOR_SCROLLABLE設置為SQL_NONSCROLLABLE時,游標僅支援"*提取方向"* 值SQL_FETCH_NEXT。  
  
## <a name="sensitivity"></a>敏感度  
 當 SQL_ATTR_CURSOR_SENSITIVITY 設定為 SQL_SENSITIVE 時，資料指標會將目前使用者所進行或其他使用者所認可的資料修改反映出來。 當 SQL_ATTR_CURSOR_SENSITIVITY 設定為 SQL_INSENSITIVE 時，資料指標不會反映資料修改。  
  
## <a name="see-also"></a>另請參閱  
 [使用游標 (ODBC)](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md) [游標屬性](properties/cursor-properties.md) 
  
  
