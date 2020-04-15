---
title: 記錄與未記錄的修改 |微軟文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], image
- data types [ODBC], text
- logged vs. nonlogged modifications [SQL Server Native Client]
- columns [ODBC]
- ODBC data types, image columns
- nonlogged vs. logged modifications
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: 20aa5b27-4a2c-46e7-8356-beb0eebf4b7e
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: dc7fb913bef4083b045a0c1c010bdedbc43135c5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297651"
---
# <a name="logged-vs-unlogged-modifications"></a>已記錄與未記錄的修改
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]應用程式可以請求本機用戶端ODBC驅動程式不記錄**文本****、ntext**和**圖像**修改。 但是在使用這個選項時，應該要特別小心。 它只應用於**文本****、ntext**或**圖像**數據不重要且資料擁有者願意權衡恢復資料的能力以獲得更高性能的情況。  
  
 **文本****、ntext**和**圖像**修改的日誌記錄通過調用[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)進行控制,*屬性*參數設置為SQL_SOPT_SS_TEXTPTR_LOGGING,ValuePtr 設置為SQL_TL_ON或SQL_TL_OFF。 *ValuePtr*  
  
## <a name="see-also"></a>另請參閱  
 [管理 Text 和 Image 資料行](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
  
