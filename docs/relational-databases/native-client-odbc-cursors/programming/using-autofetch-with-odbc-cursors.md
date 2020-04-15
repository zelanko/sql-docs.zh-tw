---
title: 將自動擷取與 ODBC 游標一起使用 |微軟文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, autofetch
- autofetch option
- cursors [ODBC], autofetch
ms.assetid: 57bd55f4-8945-4d8d-9f58-d30c81d2a514
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 812f4742dfe8273c4e96fc5205626fe1f6c07347
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298408"
---
# <a name="using-autofetch-with-odbc-cursors"></a>使用自動擷取搭配 ODBC 資料指標
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  連接到的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]實體時,[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本機客戶端 ODBC 驅動程式支援使用任何伺服器游標類型時的自動提取選項。 使用自動提取,打開游標的**SQLExecute**或**SQLExecDirect**函數還具有隱式[SQLFetchScroll(SQL_FIRST)](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)函數。 構成第一個資料列集的資料列會當做陳述式執行的一部分而傳回至繫結的應用程式變數，如此就不需要再一次透過網路往返伺服器。 啟用自動提取選項時不支援[SQLGetData;](../../../relational-databases/native-client-odbc-api/sqlgetdata.md)結果集列必須綁定到程式變數。  
  
 應用程式會藉由將驅動程式特定的 SQL_SOPT_SS_CURSOR_OPTIONS 陳述式屬性設定為 SQL_CO_AF 來要求自動擷取。  
  
## <a name="see-also"></a>另請參閱  
 [游標程式設計詳細資訊&#40;ODBC&#41;](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
