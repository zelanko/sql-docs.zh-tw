---
title: SQL 外鍵 |微軟文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLForeignKeys function
ms.assetid: 6c01ce0d-30d7-4c86-8705-3ab254d8a845
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b934ec05cf5f7b908efe83eeeb68bb358cd45156
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298475"
---
# <a name="sqlforeignkeys"></a>SQLForeignKeys
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援串聯更新，而且會透過外部索引鍵條件約束機制刪除。 如果在 FOREIGN KEY 條件約束的 ON UPDATE 和/或 ON DELETE 子句上指定 CASCADE 選項，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會針對 UPDATE_RULE 和/或 DELETE_RULE 資料行傳回 SQL_NO_ACTION。 如果在 FOREIGN KEY 條件約束的 ON UPDATE 和/或 ON DELETE 子句上指定 NO ACTION 選項，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會針對 UPDATE_RULE 和/或 DELETE_RULE 資料行傳回 SQL_NO_ACTION。  
  
 當任何**SQL 外鍵**參數中存在無效值時 **,SQL 外鍵**在執行時返回SQL_SUCCESS。 當在這些參數中使用無效值時 **,SQLFetch**將返回SQL_NO_DATA。  
  
 **SQL 外交金鑰**可以在靜態伺服器游標上執行。 嘗試在可向上(動態或鍵集)游標上執行**SQL 外鍵**將返回SQL_SUCCESS_WITH_INFO指示游標類型已更改。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 ODBC 驅動程式透過接受*FKCatalogName*和*PKCatalogName*參數的兩部分名稱 *(Linked_Server_Name.Catalog_Name)* 支援報告連結伺服器上的表的資訊。  
  
## <a name="see-also"></a>另請參閱  
 [SQL 外鍵函數](https://go.microsoft.com/fwlink/?LinkId=59344)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
