---
title: SQLEndTran |Microsoft Docs
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d272a26558aa163f8168288f95da8036666b9277
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2019
ms.locfileid: "73786937"
---
# <a name="sqlendtran"></a>SQLEndTran
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  根據預設，當**SQLEndTran**認可或回復作業時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驅動程式會關閉語句的相關資料指標。 除非伺服器資料指標是靜態的，否則會關閉它們。 當**SQLEndTran**認可或回復作業時，語句相關資料指標的行為是由驅動程式特定的 ODBC 連接屬性值所決定，SQL_COPT_SS_PRESERVE_CURSORS，由[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)設定。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 的執行詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [SQLEndTran 函式](https://go.microsoft.com/fwlink/?LinkId=59342)  
  
  
