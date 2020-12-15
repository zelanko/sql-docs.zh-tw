---
description: 繫結與未繫結的 Text 和 Image 資料行
title: 系結與未系結的 Text 和 Image 資料行 |Microsoft Docs
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
- columns [ODBC]
- ODBC data types, image columns
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: ffd3442e-d880-46e9-b848-2365a09a2406
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e6784e70d84927721eeab15d715221c519bdb1ae
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97473479"
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>繫結與未繫結的 Text 和 Image 資料行
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  使用伺服器資料指標時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式會經過優化，不會在執行 **SQLFetch** 時傳輸未系結之 **text**、 **Ntext** 或 **image** 資料行的資料。 在應用程式發出資料行的 [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)之前，不會實際從伺服器取出 **text**、 **Ntext** 或 **image** 資料。  
  
 您可以撰寫許多應用程式，如此一來，當使用者只是在資料指標中向上和向下滾動時，就不會顯示任何 **text**、 **Ntext** 或 **image** 資料。 當使用者選取資料列以取得更多詳細資料時，應用程式可以呼叫 **SQLGetData** 來取得 **text**、 **Ntext** 或 **image** 資料。 這會防止針對使用者未選取的任何資料列傳送 **text**、 **Ntext** 或 **image** 資料，因此可防止傳輸非常大量的資料。  
  
## <a name="see-also"></a>另請參閱  
 [管理 Text 和 Image 資料行](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)   
 [資料指標行為](../../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)  
  
  
