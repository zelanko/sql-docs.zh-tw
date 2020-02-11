---
title: 日期和時間改善（ODBC） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- date/time [ODBC]
- ODBC, date/time improvements
ms.assetid: e31d5ca5-2103-498f-954c-1ee93e217186
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d56689bb045a6540bfdfbb9c7147dc34db110bde
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63207001"
---
# <a name="date-and-time-improvements-odbc"></a>日期和時間改善 (ODBC)
  
  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 導入了新的日期和時間資料類型。 本章節描述如何將這些新類型公開為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 中的延伸模組。 如需有關新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]日期和時間資料類型之 Native Client 支援的總覽，請參閱[日期和時間改善](../native-client/features/date-and-time-improvements.md)。 如需示範 ODBC 日期/時間支援的範例，請參閱[使用日期和時間類型](../native-client-odbc-how-to/use-date-and-time-types.md)。  
  
 如需日期和時間資料類型的一般資訊，請參閱[datetime &#40;transact-sql&#41;](/sql/t-sql/data-types/datetime-transact-sql)。  
  
## <a name="in-this-section"></a>本節內容  
 [ODBC 日期和時間改善的資料類型支援](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md)  
 提供有關支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日期和時間資料類型之 ODBC 類型的資訊。  
  
 [&#40;ODBC&#41;的中繼資料](../../database-engine/dev-guide/metadata-odbc.md)  
 描述在實作參數描述項 (IPD) 和實作資料列描述項 (IRD) 欄位中傳回的資訊，以及 `SQLColumns` 和 `SQLProcedureColumns` 傳回的資料行中繼資料。 也會描述 `SQLGetTypeInfo` 所傳回的資料類型中繼資料。  
  
 [&#40;ODBC&#41;的日期時間資料類型轉換](datetime-data-type-conversions-odbc.md)  
 描述如何在 datetime 和 datetimeoffset 值之間轉換。  
  
 [日期和時間類型的 SQL_variant 支援](sql-variant-support-for-date-and-time-types.md)  
 描述 SQL_VARIANT 函數對日期和時間增強功能的支援。  
  
 [增強型日期和時間類型的大量複製變更 &#40;OLE DB 和 ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)  
 描述可支援大量複製作業的日期/時間增強功能。  
  
 [舊版 SQL Server 版本的增強型日期和時間類型行為 &#40;ODBC&#41;](enhanced-date-and-time-type-behavior-with-previous-sql-server-versions-odbc.md)  
 描述當使用日期和時間增強功能的用戶端應用程式與舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 進行通訊時，以及使用舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 編譯的用戶端將命令傳送到支援日期和時間增強功能的伺服器時，將會發生的預期行為。  
  
 [增強型日期和時間功能的 ODBC API 支援](odbc-api-support-for-enhanced-date-and-time-features.md)  
 列出支援日期和時間增強功能的 ODBC 函數。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
