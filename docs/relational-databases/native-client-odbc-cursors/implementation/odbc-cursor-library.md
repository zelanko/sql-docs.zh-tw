---
title: ODBC 游標庫 |微軟文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], library
- SQL_CUR_USE_DRIVER option
- ODBC applications, cursors
- ODBC cursors, library
- SQL_CUR_USE_IF_NEEDED option
- SQLSetConnectAttr function
- SQL_CUR_USE_ODBC option
ms.assetid: 3c610d3d-6e06-49cf-9a40-05b6a1c83a32
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 93c85bc943d1a6a081cbea6bbeae40ba85aeffc5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305383"
---
# <a name="odbc-cursor-library"></a>ODBC 資料指標程式庫
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  某些 ODBC 驅動程式僅支援預設游標設定;某些 ODBC 驅動程式僅支援預設游標設置。這些驅動程式也不支援定位游標操作,如**SQLSetPos**。 ODBC 資料指標程式庫是 Microsoft 資料存取元件 (MDAC) 的元件，可用來在一般並不支援區塊或靜態資料指標的驅動程式上實作這些項目。 游標庫還為它創建的游標實現定位更新和刪除語句和**SQLSetPos。**  
  
 ODBC 資料指標程式庫會實作為 ODBC 驅動程式管理員和 ODBC 驅動程式之間的層級。 如果 ODBC 資料指標程式庫已載入，則 ODBC 驅動程式管理員會將所有與資料指標相關的命令路由到資料指標程式庫，而不是驅動程式。 資料指標程式庫會從基礎驅動程式提取整個結果集，並將結果集快取在用戶端上來實作資料指標。 使用 ODBC 資料指標程式庫時，應用程式只限於使用資料指標程式庫的資料指標功能，而無法使用基礎驅動程式中任何其他資料指標功能的支援。  
  
 您幾乎不需要藉由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式來使用 ODBC 資料指標程式庫，因為驅動程式本身所支援的資料指標功能就比 ODBC 資料指標程式庫來得多。 將 ODBC 游標[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]庫與 本機用戶端 ODBC 驅動程式結合使用的唯一原因是驅動程式通過伺服器游標實現了其游標支援,而伺服器游標不支援所有 SQL 語句。 任何時候如果需要具有預存程序、批次或 SQL 陳述式 (包含 COMPUTE、COMPUTE BY、FOR BROWSE 或 INTO) 的靜態資料指標，請考慮使用 ODBC 資料指標程式庫。 不過，使用資料指標程式庫時必須小心，因為它會將整個結果集都快取在用戶端上，這可能會耗用大量的記憶體並使效能降低。  
  
 應用程式在連接到資料源之前使用[SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)設定SQL_ATTR_ODBC_CURSORS連接屬性,從而在連接的基礎上調用游標庫。 SQL_ATTR_ODBC_CURSORS 會設定為下列三個值之一：  
  
 SQL_CUR_USE_ODBC  
 使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本機用戶端 ODBC 驅動程式設定此選項時,ODBC 游[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]標庫將覆蓋 本機用戶端 ODBC 驅動程式的本機游標支援。 連接只能使用資料指標程式庫所支援的資料指標類型，而不能使用伺服器資料指標。  
  
 SQL_CUR_USE_DRIVER  
 設定此選項後,所有支援[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本機用戶端ODBC驅動程式的遊標都可用於連接。 而不能使用 ODBC 資料指標程式庫。 所有的資料指標都會實作為伺服器資料指標。  
  
 SQL_CUR_USE_IF_NEEDED  
 設定此選項後,效果與與[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本機用戶端ODBC驅動程式一起使用時的效果相同SQL_CUR_USE_DRIVER。 在連接時,ODBC 驅動程式管理員將測試以查看是否連接到的ODBC驅動程式支援[SQLFetchScrollSQL_FETCH_PRIOR](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)選項。 如果驅動程式不支援這個選項，則 ODBC 驅動程式管理員會載入 ODBC 資料指標程式庫。 如果驅動程式支援這個選項，則 ODBC 驅動程式管理員不會載入 ODBC 資料指標程式庫，而應用程式會使用該驅動程式的原生支援。 由於[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本機用戶端ODBC驅動程式支援SQL_FETCH_PRIOR,因此ODBC驅動程式管理員不會載入ODBC游標庫。  
  
 資料指標程式庫可以讓應用程式在連接上使用多個作用中陳述式，以及可捲動且可更新的資料指標。 資料指標程式庫必須載入，才能支援這項功能。 使用[SQLSetConnect Attr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)指定如何使用游標庫,使用[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)來指定游標類型、併發和行集大小。  
  
## <a name="see-also"></a>另請參閱  
 [如何實作資料指標](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
  
