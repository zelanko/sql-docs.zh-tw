---
title: 日期和時間改善 (OLE DB) |Microsoft Docs
description: 日期和時間改善 (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB]
- OLE DB, date/time improvements
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 5518461fade08e6f23e1594056c284865957274c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66769334"
---
# <a name="date-and-time-improvements-ole-db"></a>日期和時間改善 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 導入了新的日期和時間資料類型。 本章節描述如何這些新類型公開為 OLE DB 驅動程式中的延伸模組適用於 SQL Server。 如需 OLE DB Driver for SQL Server 支援新的日期和時間資料類型的概觀，請參閱 <<c0> [ 日期和時間改善](../../oledb/features/date-and-time-improvements.md)。 如需範例，請參閱[使用增強型日期和時間功能&#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-enhanced-date-and-time-features-ole-db.md)。  
  
 一般日期和時間資料類型的詳細資訊，請參閱[datetime &#40;TRANSACT-SQL&#41;](../../../t-sql/data-types/datetime-transact-sql.md)。  
  
## <a name="in-this-section"></a>本節內容  
 [對 OLE DB 日期和時間改善的資料類型支援](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)  
 提供 OLE DB (OLE DB Driver for SQL Server) 的相關資訊類型支援[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]日期和時間資料類型。  
  
 [Metadata &#40;OLE DB&#41;](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)  
 包含有關 DBBINDING 結構、 資訊**icommandwithparameters:: Getparameterinfo**， **icommandwithparameters:: Setparameterinfo**， **IColumnsRowset::GetColumnsRowset**，接著**ColumnsInfo::GetColumnInfo**。 同時提供有關 OLE DB 結構描述資料列集更新的資訊。  
  
 [繫結和轉換 &#40;OLE DB&#41;](../../oledb/ole-db-date-time/conversions-ole-db.md)  
 描述在伺服器和用戶端之間，針對現有日期類型和新日期類型進行轉換的規則。  
  
 [增強型日期和時間類型的大量複製變更 &#40;OLE DB&#41;](../../oledb/ole-db-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db.md)  
 描述可支援大量複製作業的日期/時間增強功能。  
  
 [OLE DB API 對日期和時間增強功能的支援](../../oledb/ole-db-date-time/ole-db-api-support-for-date-and-time-enhancements.md)  
 描述支援日期/時間增強功能的 OLE DB API。  
  
 [IRowsetFind 的相容性](../../oledb/ole-db-date-time/comparability-for-irowsetfind.md)  
 描述日期/時間類型和**IRowsetFind**。  
 
  
## <a name="see-also"></a>另請參閱  
 [OLE DB Driver for SQL Server 程式設計](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
