---
description: 資料指標行為
title: 資料指標行為 |Microsoft Docs
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 91bc7286beb8b03f6e76698e84a8fcf3d8d3f11c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97438661"
---
# <a name="cursor-behaviors"></a>資料指標行為
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  ODBC 透過指定資料指標的可捲動性和敏感度，支援指定其行為的 ISO 選項。 這些行為是藉由在 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)的呼叫上設定 SQL_ATTR_CURSOR_SCROLLABLE 和 SQL_ATTR_CURSOR_SENSITIVITY 選項來指定。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會要求包含下列特性的伺服器資料指標，藉以實作這些選項。  
  
|資料指標行為設定|要求的伺服器資料指標特性|  
|------------------------------|---------------------------------------------|  
|SQL_SCROLLABLE 和 SQL_SENSITIVE|索引鍵集驅動資料指標和以版本為基礎的開放式並行存取|  
|SQL_SCROLLABLE 和 SQL_INSENSITIVE|靜態資料指標和唯讀並行存取|  
|SQL_SCROLLABLE 和 SQL_UNSPECIFIED|靜態資料指標和唯讀並行存取|  
|SQL_NONSCROLLABLE 和 SQL_SENSITIVE|順向資料指標和以版本為基礎的開放式並行存取|  
|SQL_NONSCROLLABLE 和 SQL_INSENSITIVE|預設結果集 (順向、唯讀)|  
|SQL_NONSCROLLABLE 和 SQL_UNSPECIFIED|預設結果集 (順向、唯讀)|  
  
 以版本為基礎的開放式平行存取需要基礎資料表中的 **時間戳記** 資料行。 如果在沒有 **時間戳記** 資料行的資料表上要求以版本為基礎的開放式並行存取控制，則伺服器會使用以值為基礎的開放式平行存取。  
  
## <a name="scrollability"></a>可捲動性  
 當 SQL_ATTR_CURSOR_SCROLLABLE 設定為 SQL_SCROLLABLE 時，資料指標會針對 [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)的 *FetchOrientation* 參數支援所有不同的值。 當 SQL_ATTR_CURSOR_SCROLLABLE 設定為 SQL_NONSCROLLABLE 時，資料指標只支援 SQL_FETCH_NEXT 的 *FetchOrientation* 值。  
  
## <a name="sensitivity"></a>敏感度  
 當 SQL_ATTR_CURSOR_SENSITIVITY 設定為 SQL_SENSITIVE 時，資料指標會將目前使用者所進行或其他使用者所認可的資料修改反映出來。 當 SQL_ATTR_CURSOR_SENSITIVITY 設定為 SQL_INSENSITIVE 時，資料指標不會反映資料修改。  
  
## <a name="see-also"></a>另請參閱  
 [使用資料指標 (ODBC) ](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)資料 [指標屬性](properties/cursor-properties.md) 
  
  
