---
title: SQLTable 特權 |微軟文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLTablePrivileges function
ms.assetid: 8cce22d5-28b1-4b50-a5bc-1de03e0ffd6b
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d7a77eb5ea151c3a85f2235f48bb03d0e98dd9ce
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81291898"
---
# <a name="sqltableprivileges"></a>SQLTablePrivileges
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **SQLTable 特權**可以在靜態游標上執行。 嘗試在可提升的(鍵集驅動或動態)上執行**SQLTable 特權**,SQL_SUCCESS_WITH_INFO指示游標類型已更改。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 ODBC 驅動程式通過接受*目錄名稱*參數的兩部分名稱 *(Linked_Server_Name.Catalog_Name)* 支援報告連結伺服器上的表的資訊。  
  
## <a name="see-also"></a>另請參閱  
 [SQLTable 特權函數](https://go.microsoft.com/fwlink/?LinkId=59373\)   
 [ODBC API 實作詳細資料](~/relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
