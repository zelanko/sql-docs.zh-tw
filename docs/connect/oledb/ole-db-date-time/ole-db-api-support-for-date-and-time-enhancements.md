---
title: API 對日期和時間增強功能的支援 (OLE DB 驅動程式)
description: 了解支援增強日期/時間功能的 OLE DB API，包括函式名稱與描述。
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8209c1b1ca6f3c00ce4cd10455c35c8b9d4dfad4
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862355"
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>OLE DB API 對日期和時間增強功能的支援
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  下列 OLE DB API 支援日期/時間增強功能。  
  
|函式|描述|  
|--------------|-----------------|  
|IAccessor::CreateAccessor|在 DBBINDING 結構中新增一個旗標，讓應用程式可以區分 **datetime**、**datetime2** 及 **smalldatetime** 值。 如需詳細資訊，請參閱[參數和資料列集中繼資料](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|IBCPSession::BCPColFmt|如需詳細資訊，請參閱[增強型日期和時間類型的大量複製變更 &#40;OLE DB&#41;](../../oledb/ole-db-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db.md)。|  
|ICommandWithParameters::GetParameterInfo|如需詳細資訊，請參閱[參數和資料列集中繼資料](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|ICommandWithParameters::SetParameterinfo|如需詳細資訊，請參閱[參數和資料列集中繼資料](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|IColumnsRowset::GetColumnsRowset|如需詳細資訊，請參閱[參數和資料列集中繼資料](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|IColumnsInfo::GetColumnInfo|如需詳細資訊，請參閱[參數和資料列集中繼資料](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|IDBSchemaRowset::GetRowset|如需受影響結構描述資料列集的詳細資訊，請參閱[日期和時間以及結構描述資料列集](../../oledb/ole-db-date-time/metadata-date-and-time-and-schema-rowsets.md)。|  
|IRowsetFastLoad|此介面支援新的日期/時間類型，但是它的介面沒有任何變更。|  
|ITableDefinition::CreateTable|如需詳細資訊，請參閱[對 OLE DB 日期和時間改善的資料類型支援](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)。|  
  
## <a name="see-also"></a>另請參閱  
 [日期和時間改善 &#40;OLE DB&#41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
