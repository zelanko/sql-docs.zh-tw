---
title: ODBC 資料指標程式庫 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: eeaef25c0a7c1d09ca3ee52cee2783275aa6133e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "73784726"
---
# <a name="odbc-cursor-library"></a>ODBC 資料指標程式庫
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  某些 ODBC 驅動程式只支援預設的資料指標設定;這些驅動程式也不支援定位的資料指標作業，例如**SQLSetPos**。 ODBC 資料指標程式庫是 Microsoft 資料存取元件 (MDAC) 的元件，可用來在一般並不支援區塊或靜態資料指標的驅動程式上實作這些項目。 資料指標程式庫也會針對它所建立的資料指標，執行定位的 UPDATE 和 DELETE 子句和**SQLSetPos** 。  
  
 ODBC 資料指標程式庫會實作為 ODBC 驅動程式管理員和 ODBC 驅動程式之間的層級。 如果 ODBC 資料指標程式庫已載入，則 ODBC 驅動程式管理員會將所有與資料指標相關的命令路由到資料指標程式庫，而不是驅動程式。 資料指標程式庫會從基礎驅動程式提取整個結果集，並將結果集快取在用戶端上來實作資料指標。 使用 ODBC 資料指標程式庫時，應用程式只限於使用資料指標程式庫的資料指標功能，而無法使用基礎驅動程式中任何其他資料指標功能的支援。  
  
 您幾乎不需要藉由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式來使用 ODBC 資料指標程式庫，因為驅動程式本身所支援的資料指標功能就比 ODBC 資料指標程式庫來得多。 使用 ODBC 資料指標程式庫搭配[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驅動程式的唯一理由是，驅動程式會透過伺服器資料指標來執行其資料指標支援，而伺服器資料指標並不支援所有的 SQL 語句。 任何時候如果需要具有預存程序、批次或 SQL 陳述式 (包含 COMPUTE、COMPUTE BY、FOR BROWSE 或 INTO) 的靜態資料指標，請考慮使用 ODBC 資料指標程式庫。 不過，使用資料指標程式庫時必須小心，因為它會將整個結果集都快取在用戶端上，這可能會耗用大量的記憶體並使效能降低。  
  
 應用程式會在連接到資料來源之前，使用[SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)來設定 SQL_ATTR_ODBC_CURSORS 連接屬性，藉以依連接叫用游標程式庫。 SQL_ATTR_ODBC_CURSORS 會設定為下列三個值之一：  
  
 SQL_CUR_USE_ODBC  
 當此選項設定為[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] NATIVE client odbc 驅動程式時，ODBC 資料指標程式庫會[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]覆寫 native client odbc 驅動程式的原生資料指標支援。 連接只能使用資料指標程式庫所支援的資料指標類型，而不能使用伺服器資料指標。  
  
 SQL_CUR_USE_DRIVER  
 當設定這個選項時， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驅動程式的原生支援的所有資料指標都可以用於連接。 而不能使用 ODBC 資料指標程式庫。 所有的資料指標都會實作為伺服器資料指標。  
  
 SQL_CUR_USE_IF_NEEDED  
 當設定這個選項時，與[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驅動程式搭配使用時，效果會與 SQL_CUR_USE_DRIVER 相同。 在連線時間，ODBC 驅動程式管理員會測試是否已連接 ODBC 驅動程式，以支援[SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)的 SQL_FETCH_PRIOR 選項。 如果驅動程式不支援這個選項，則 ODBC 驅動程式管理員會載入 ODBC 資料指標程式庫。 如果驅動程式支援這個選項，則 ODBC 驅動程式管理員不會載入 ODBC 資料指標程式庫，而應用程式會使用該驅動程式的原生支援。 因為[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驅動程式支援 SQL_FETCH_PRIOR，所以 Odbc 驅動程式管理員不會載入 odbc 資料指標程式庫。  
  
 資料指標程式庫可以讓應用程式在連接上使用多個作用中陳述式，以及可捲動且可更新的資料指標。 資料指標程式庫必須載入，才能支援這項功能。 使用[SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)來指定資料指標程式庫的使用方式，並[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)以指定資料指標類型、並行和資料列集大小。  
  
## <a name="see-also"></a>另請參閱  
 [如何實作資料指標](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
  
