---
title: SQLSetEnvAttr | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLSetEnvAttr function
ms.assetid: d4114571-feca-4330-b2e4-7bfd1050b812
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0c968499ab546d4e2aeb168cb6a039618eb3d5bc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63014210"
---
# <a name="sqlsetenvattr"></a>SQLSetEnvAttr
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [ODBC 程式設計人員參考](https://go.microsoft.com/fwlink/?LinkId=45250)定義如何解譯 ODBC 驅動程式應該**SQLSetEnvAttr**屬性從撰寫 ODBC 2 的應用程式的規格。*x*或 ODBC 3。*x* API。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式符合這些規則。  
  
 其中一個屬性所控制**SQLSetEnvAttr**這是連接共用是否要使用。 如果連接共用搭配[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式， *DriverCompletion*參數必須設定為 sql_driver_noprompt 時，使用 進行連接時[SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md)或**SQLConnect**。  
  
## <a name="see-also"></a>另請參閱  
 [SQLSetEnvAttr 函數](https://go.microsoft.com/fwlink/?LinkId=59369)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
