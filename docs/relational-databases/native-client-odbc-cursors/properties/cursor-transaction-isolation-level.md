---
title: 資料指標交易隔離等級 |Microsoft Docs
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
- isolation levels [ODBC]
- ODBC applications, row versioning
- cursors [ODBC], isolation levels
- ODBC cursors, isolation levels
- row versioning [SQL Server], ODBC
ms.assetid: 0c6663a4-5a25-44aa-8fe4-e35af9bf4a83
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 676c47c243126b4915024c10d3fee5c4ae5bca6d
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43059371"
---
# <a name="cursor-transaction-isolation-level"></a>資料指標交易隔離等級
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  資料指標的完整鎖定行為是以並行屬性之間的互動以及用戶端所設定的交易隔離等級為基礎。 ODBC 用戶端設定交易隔離層級使用[SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) SQL_ATTR_TXN_ISOLATION 或 SQL_COPT_SS_TXN_ISOLATION 屬性。 特定資料指標環境的鎖定行為藉由結合以下各項來決定：並行的鎖定行為，以及交易隔離層級選項。  
  
 下列的資料指標交易隔離等級都受到[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式：  
  
-   讀取認可 (SQL_TXN_READ_COMMITTED)  
  
-   讀取未認可 (SQL_TXN_READ_UNCOMMITTED)  
  
-   可重覆讀取 (SQL_TXN_REPEATABLE_READ)  
  
-   可序列化 (SQL_TXN_SERIALIZABLE)  
  
-   快照集 (SQL_TXN_SS_SNAPSHOT)  
  
 請注意，ODBC API 會指定其他交易隔離等級，但是這些不會受到[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]或[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式。  
  
## <a name="see-also"></a>另請參閱  
 [資料指標屬性](../../../relational-databases/native-client-odbc-cursors/properties/cursor-properties.md)  
  
  
