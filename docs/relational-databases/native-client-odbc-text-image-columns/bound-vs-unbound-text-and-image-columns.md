---
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 11a7e27e7adce8f87986571c2029d37c82e319b3
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86012318"
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>繫結與未繫結的 Text 和 Image 資料行
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  使用伺服器資料指標時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式已優化，而不會在執行**SQLFetch**時傳送未系結之**text**、 **Ntext**或**image**資料行的資料。 在應用程式發出資料行的[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)之前，不會實際從伺服器抓取**text**、 **Ntext**或**image**資料。  
  
 許多應用程式都可以撰寫，如此一來，使用者只要在資料指標中上下滾動，就不會顯示任何**文字**、 **Ntext**或**影像**資料。 當使用者選取資料列以取得更多詳細資料時，應用程式就可以呼叫**SQLGetData**來捕獲**text**、 **Ntext**或**image**資料。 這會防止針對使用者未選取的任何資料列傳輸**text**、 **Ntext**或**image**資料，因此可防止傳輸非常大量的資料。  
  
## <a name="see-also"></a>另請參閱  
 [管理 Text 和 Image 資料行](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)   
 [資料指標行為](../../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)  
  
  
