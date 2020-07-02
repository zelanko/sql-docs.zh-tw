---
title: 如何實作為資料指標 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- ODBC cursors, about ODBC cursors
- ODBC applications, cursors
- cursors [ODBC], about ODBC cursors
ms.assetid: 2b1d7dd4-08a4-43fc-b3eb-70c183d0941f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e45967508fe46dd859bf728eded8814309ca9be0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85719780"
---
# <a name="how-cursors-are-implemented"></a>如何實作資料指標
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  ODBC 應用程式會在執行 SQL 陳述式之前設定一或多個陳述式屬性，藉此來控制資料指標的行為。 ODBC 有兩個不同的方法可指定資料指標的特性：  
  
-   資料指標類型  
  
     資料指標類型是使用[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)的 SQL_ATTR_CURSOR_TYPE 屬性來設定。 ODBC 資料指標類型為順向、靜態、索引鍵集驅動、混合式和動態。 設定資料指標類型是在 ODBC 中指定資料指標的原始方法。  
  
-   資料指標行為  
  
     資料指標行為是使用**SQLSetStmtAttr**的 SQL_ATTR_CURSOR_SCROLLABLE 和 SQL_ATTR_CURSOR_SENSITIVITY 屬性來設定。 這些屬性是根據 ISO 標準中針對 DECLARE CURSOR 陳述式定義的 SCROLL 和 SENSITIVE 關鍵字來模型化。 這兩個 ISO 選項是在 ODBC 3.0 版中導入。  
  
 應該使用這兩個方法的其中一個來指定 ODBC 資料指標的特性，並將喜好設定設定為 ODBC 資料指標類型。  
  
 除了設定資料指標的類型以外，ODBC 應用程式也會設定其他選項，例如每一個提取所傳回的資料列數、並行選項和交易隔離等級。 可以針對 ODBC 樣式的資料指標 (順向、靜態、索引鍵集驅動、混合式和動態) 或 ISO 樣式的資料指標 (可捲動性和敏感性) 來設定這些選項。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式支援數種實際執行各種類型資料指標的方式。 此驅動程式會使用預設 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 結果集來實作某些類型的資料指標，並使用 ODBC 資料指標程式庫將其他類型實作為伺服器資料指標。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [使用 QL Server 預設結果集](../../../relational-databases/native-client-odbc-cursors/implementation/using-sql-server-default-result-sets.md)  
  
-   [使用伺服器資料指標](../../../relational-databases/native-client-odbc-cursors/implementation/using-server-cursors.md)  
  
-   [ODBC 資料指標程式庫](../../../relational-databases/native-client-odbc-cursors/implementation/odbc-cursor-library.md)  
  
## <a name="see-also"></a>另請參閱  
 [&#40;ODBC&#41;使用資料指標](../../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  
