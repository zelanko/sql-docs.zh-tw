---
title: 日期和時間改進 (ODBC) |微軟文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- date/time [ODBC]
- ODBC, date/time improvements
ms.assetid: e31d5ca5-2103-498f-954c-1ee93e217186
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 94a9b8517ebd2539250995fea896c53a376fc65d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301748"
---
# <a name="date-and-time-improvements-odbc"></a>日期和時間改善 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 導入了新的日期和時間資料類型。 本章節描述如何將這些新類型公開為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 中的延伸模組。 有關新日期和時間資料類型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的本機客戶端支援的概述,請參閱[日期和時間改進](../../relational-databases/native-client/features/date-and-time-improvements.md)。 有關展示 ODBC 日期/時間支援的範例,請參閱[使用日期和時間類型](../../relational-databases/native-client-odbc-how-to/use-date-and-time-types.md)。  
  
 如需更多日期和時間資料類型的一般資訊，請參閱 [datetime &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md)。  
  
## <a name="in-this-section"></a>本節內容  
 [資料類型對 ODBC 日期和時間支援的改善](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md)  
 提供有關支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日期和時間資料類型之 ODBC 類型的資訊。  
  
 [中繼資料&#40;ODBC&#41;](https://msdn.microsoft.com/library/99133efc-b1f2-46e9-8203-d90c324a8e4c)  
 描述在實現參數描述符 (IPD) 和實現行描述符 (IRD) 欄位中傳回的資訊,以及**SQLColumn**和**SQLAAColumn**傳回的欄元資料。 還描述了**SQLGetTypeInfo**傳回的數據類型元資料。  
  
 [日期時間資料型別轉換&#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-odbc.md)  
 描述如何在 datetime 和 datetimeoffset 值之間轉換。  
  
 [日期和時間類型的 sql_variant 支援](../../relational-databases/native-client-odbc-date-time/sql-variant-support-for-date-and-time-types.md)  
 描述 SQL_VARIANT 函數對日期和時間增強功能的支援。  
  
 [用於增強日期和時間類型的批次複製變更,&#40;OLE DB 和 ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)  
 描述可支援大量複製作業的日期/時間增強功能。  
  
 [具有早期 SQL 伺服器版本的增強的日期和時間類型行為&#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/enhanced-date-and-time-type-behavior-with-previous-sql-server-versions-odbc.md)  
 描述當使用日期和時間增強功能的用戶端應用程式與舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 進行通訊時，以及使用舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 編譯的用戶端將命令傳送到支援日期和時間增強功能的伺服器時，將會發生的預期行為。  
  
 [增強型日期和時間功能的 ODBC API 支援](../../relational-databases/native-client-odbc-date-time/odbc-api-support-for-enhanced-date-and-time-features.md)  
 列出支援日期和時間增強功能的 ODBC 函數。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
