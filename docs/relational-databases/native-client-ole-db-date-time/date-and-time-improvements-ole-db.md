---
title: 日期和時間改善（OLE DB） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB]
- OLE DB, date/time improvements
ms.assetid: 71614aaf-0fa4-4fe0-b522-68e2e0b66f43
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c1ac0b0d93c35986b3eeedaf7148339770af1933
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2019
ms.locfileid: "73772809"
---
# <a name="date-and-time-improvements-ole-db"></a>日期和時間改善 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 導入了新的日期和時間資料類型。 本章節描述如何將這些新類型公開為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 中的延伸模組。 如需新日期和時間資料類型之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 支援的總覽，請參閱[日期和時間改善](../../relational-databases/native-client/features/date-and-time-improvements.md)。 如需範例，請參閱[使用增強的日期和&#40;時間&#41;功能 OLE DB](../../relational-databases/native-client-ole-db-how-to/use-enhanced-date-and-time-features-ole-db.md)。  
  
 如需日期和時間資料類型的一般資訊，請[參閱&#40;datetime transact-sql&#41;](../../t-sql/data-types/datetime-transact-sql.md)。  
  
## <a name="in-this-section"></a>本節內容  
 [對 OLE DB 日期和時間改善的資料類型支援](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)  
 提供支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日期和時間資料類型之 OLE DB （[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client）類型的相關資訊。  
  
 [中繼資料 &#40;OLE DB&#41;](https://msdn.microsoft.com/library/605e3be5-aeea-4573-9847-b866ed3c8bff)  
 包含 DBBINDING 結構、 **ICommandWithParameters：： GetParameterInfo**、 **ICommandWithParameters：： SetParameterInfo**、 **IColumnsRowset：： GetColumnsRowset**和 I**ColumnsInfo：： GetColumnInfo 的相關資訊。** . 同時提供有關 OLE DB 結構描述資料列集更新的資訊。  
  
 [繫結和轉換 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/conversions-ole-db.md)  
 描述在伺服器和用戶端之間，針對現有日期類型和新日期類型進行轉換的規則。  
  
 [增強型日期和時間類型&#40;的大量複製變更 OLE DB 和 ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)  
 描述可支援大量複製作業的日期/時間增強功能。  
  
 [OLE DB API 對日期和時間增強功能的支援](../../relational-databases/native-client-ole-db-date-time/ole-db-api-support-for-date-and-time-enhancements.md)  
 描述支援日期/時間增強功能的 OLE DB API。  
  
 [IRowsetFind 的相容性](../../relational-databases/native-client-ole-db-date-time/comparability-for-irowsetfind.md)  
 描述日期/時間類型和**IRowsetFind**。  
  
 [先前 SQL Server 版本&#40;的新日期和時間功能 OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/new-date-and-time-features-with-previous-sql-server-versions-ole-db.md)  
 描述使用日期和時間增強功能的應用程式與舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 進行通訊時，以及使用舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 編譯的用戶端將命令傳送到支援日期和時間增強功能的伺服器時的預期行為。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
