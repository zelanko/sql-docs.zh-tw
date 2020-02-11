---
title: SQLSetEnvAttr |Microsoft Docs
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8e1d8e6ea962f5cd8fe094fca195a2fa59a5701d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "73785640"
---
# <a name="sqlsetenvattr"></a>SQLSetEnvAttr
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Odbc 程式設計[人員參考](https://go.microsoft.com/fwlink/?LinkId=45250)會定義 odbc 驅動程式應該如何解讀寫入 odbc 2 之應用程式的**SQLSetEnvAttr**屬性規格。*x*或 ODBC 3。*x* API。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驅動程式符合這些規則。  
  
 **SQLSetEnvAttr**所控制的其中一個屬性就是是否要使用連接共用。 如果連接共用與[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驅動程式搭配使用，則在連接[SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md)或**SQLConnect**時， *DriverCompletion*參數必須設定為 SQL_DRIVER_NOPROMPT。  
  
## <a name="see-also"></a>另請參閱  
 [SQLSetEnvAttr 函式](https://go.microsoft.com/fwlink/?LinkId=59369)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
