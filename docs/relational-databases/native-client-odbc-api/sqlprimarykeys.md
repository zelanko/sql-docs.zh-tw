---
title: SQL 主鍵 |微軟文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLPrimaryKeys function
ms.assetid: bc61cd5b-d2f4-4f87-abc7-743cf9ea772d
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2695d253030f13f71785046a25997ec6ee768622
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288978"
---
# <a name="sqlprimarykeys"></a>SQLPrimaryKeys
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  表可能具有可用作唯一行標識符的列或列,在沒有「主要密鑰」約束的情況下創建的表將空結果集返回到 SQLPrimaryKeys。 ODBC 函數[SQL 特別列](../../relational-databases/native-client-odbc-api/sqlspecialcolumns.md)報沒有主鍵的表的行標識符候選項。  
  
 SQL 主要金鑰SQL_SUCCESS*目錄名稱*、*架構名稱*參數或*表名*參數是否存在值。 當這些參數中使用無效值時，SQLFetch 會傳回 SQL_NO_DATA。  
  
 SQL主要密鑰可以在靜態伺服器游標上執行。 嘗試在可上升(動態或鍵集)游標上執行 SQLPrimaryKeys 將返回SQL_SUCCESS_WITH_INFO指示游標類型已更改。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 ODBC 驅動程式通過接受*目錄名稱*參數的兩部分名稱 *(Linked_Server_Name.Catalog_Name)* 支援報告連結伺服器上的表的資訊。  
  
## <a name="sqlprimarykeys-and-table-valued-parameters"></a>SQLPrimaryKeys 和資料表值參數  
 如果語句屬性SQL_SOPT_SS_NAME_SCOPE具有值SQL_SS_NAME_SCOPE_TABLE_TYPE,而不是其預設值SQL_SS_NAME_SCOPE_TABLE,SQLPrimaryKeys 將返回有關表類型的主要鍵列的資訊。 有關SQL_SOPT_SS_NAME_SCOPE的詳細資訊,請參閱[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。  
  
 有關表值參數的詳細資訊,請參閱[&#40;ODBC&#41;的表值參數](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL 主鍵函數](https://go.microsoft.com/fwlink/?LinkId=59361)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
