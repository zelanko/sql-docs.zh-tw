---
title: SQLSetEnvAttr |微軟文件
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6d0e93e73de0698e8bce1cb4073458cafe526c41
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301867"
---
# <a name="sqlsetenvattr"></a>SQLSetEnvAttr
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [ODBC 程式設計師的參考](https://go.microsoft.com/fwlink/?LinkId=45250)定義 ODBC 驅動程式應如何從寫入 ODBC 2 的應用程式解釋**SQLSetEnvAttr**屬性規範。*x*或 ODBC 3。*x* API。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端ODBC驅動程式符合這些規則。  
  
 **SQLSetEnvAttr**控制的屬性之一是是否使用連接池。 如果連接池與[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 ODBC 驅動程式一起使用,則在連接[SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md)或**SQLConnect**時,必須將*驅動程式完成*參數設定為SQL_DRIVER_NOPROMPT。  
  
## <a name="see-also"></a>另請參閱  
 [SQLSetEnvAttr 函數](https://go.microsoft.com/fwlink/?LinkId=59369)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
