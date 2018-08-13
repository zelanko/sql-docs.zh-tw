---
title: 配置連接控制代碼 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC applications, passwords
- ODBC applications, connections
- handles [SQL Server Native Client]
- expiration [SQL Server Native Client]
- passwords [SQL Server], modifying
- SQL Server Native Client ODBC driver, connection handles
- connection handles [SQL Server Native Client]
- modifying passwords
- SQLAllocHandle function
ms.assetid: 471d8a31-199c-4f92-bb10-004fc7733b35
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: bfe292679e8ae491cd5bc708ac8dda830d540a6c
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39563522"
---
# <a name="allocating-a-connection-handle"></a>配置連接控制代碼
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  在應用程式可以連接到資料來源或驅動程式之前，必須配置連接控制代碼。 這是藉由呼叫**SQLAllocHandle**具有*HandleType*參數設定為 SQL_HANDLE_DBC 並*InputHandle*指向初始化的環境控制代碼。  
  
 連接的特性是藉由設定連接屬性來控制。 例如，因為交易發生在連接層級，所以交易隔離等級是連接屬性。 同樣地，登入逾時 (也就是要在嘗試連接時，在逾時之前等候的秒數) 也是連接屬性。  
  
 設定連接屬性[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)，其目前的設定會擷取與[SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md)。 如果**SQLSetConnectAttr**會嘗試連接之前呼叫，ODBC 驅動程式管理員在其連接結構中儲存屬性和設定這些驅動程式中的連線程序的一部分。 有些連接屬性必須在應用程式嘗試連接之前設定，其他的屬性則可以在連接完成之後設定。 例如，SQL_ATTR_ODBC_CURSORS 必須在進行連接之前設定，但 SQL_ATTR_AUTOCOMMIT 可以在連接之後設定。  
  
 針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 版或更新版本執行的應用程式，有時可以藉由重設表格式資料流 (TDS) 網路封包大小來改善其效能。 預設封包大小是 4 KB，設定於伺服器。 4 KB 到 8 KB 的封包大小一般可提供最佳效能。 如果測試顯示應用程式使用其他封包大小時效能較佳，則可以重設封包大小。 ODBC 應用程式可以執行這項操作之前連接藉由呼叫**SQLSetConnectAttr** SQL_ATTR_PACKET_SIZE 選項。 有些應用程式在使用較大封包大小時效能較佳，但一般而言，封包大小大於 8 KB 時所能改進的效能微乎其微。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式具有一些擴充的連接屬性，應用程式可以用來增加其功能。 這其中有些屬性所控制的選項，可在資料來源中指定並用來覆寫資料來源中所設的任何選項。 例如，如果應用程式使用引號識別碼，則可以將驅動程式特定的屬性 SQL_COPT_SS_QUOTED_IDENT 設為 SQL_QI_ON，以確保一定可以設定此選項，不論資料來源中的設定為何。  
  
## <a name="see-also"></a>另請參閱  
 [與 SQL Server 通訊&#40;ODBC&#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
