---
title: SQLEndTran | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLEndTran function
ms.assetid: 95cff841-c2d5-4e1e-a18d-f3d4696a5b85
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bd7a2f26e77b475866d508cb3fa5664662f41ef4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63014572"
---
# <a name="sqlendtran"></a>SQLEndTran
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  根據預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會關閉的陳述式相關聯的資料指標時**SQLEndTran**認可或回復作業。 除非伺服器資料指標是靜態的，否則會關閉它們。 當**SQLEndTran**認可或回復作業，此陳述式相關聯的資料指標的行為取決於所設定的驅動程式專屬ODBC連接屬性SQL_COPT_SS_PRESERVE_CURSORS的值[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [SQLEndTran 函式](https://go.microsoft.com/fwlink/?LinkId=59342)  
  
  
