---
title: SQLColumn 特權 |微軟文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLColumnPrivileges function
ms.assetid: c78acd4e-8668-4abc-9bc9-6ad381965863
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9e8197e0a9b105ea6236666a82624ecd97a80568
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302599"
---
# <a name="sqlcolumnprivileges"></a>SQLColumnPrivileges
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **SQLColumn 特權**傳回SQL_SUCCESS*目錄名稱*、*架構名稱*、*表名*或*列名*參數是否存在值。 當在這些參數中使用無效值時 **,SQLFetch**將返回SQL_NO_DATA。  
  
 **SQLColumn 特權**可以在靜態伺服器游標上執行。 嘗試在可提升(動態或鍵集)游標上執行**SQLColumn 特權**將返回SQL_SUCCESS_WITH_INFO指示游標類型已更改。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 ODBC 驅動程式通過接受*目錄名稱*參數的兩部分名稱 *(Linked_Server_Name.Catalog_Name)* 支援報告連結伺服器上的表的資訊。  
  
## <a name="see-also"></a>另請參閱  
 [SQLColumn 特權函數](https://go.microsoft.com/fwlink/?LinkId=59335)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
