---
title: OLE DB API 對日期和時間增強功能的支援 | Microsoft Docs
description: OLE DB API 對日期和時間增強功能的支援
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 022f7814263067eaa3030ae6c376f99666ad0dd3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47695826"
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>OLE DB API 對日期和時間增強功能的支援
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  下列 OLE DB API 支援日期/時間增強功能。  
  
|函數|Description|  
|--------------|-----------------|  
|Iaccessor:: Createaccessor|若要啟用應用程式可以區分 DBBINDING 結構中加入旗標**datetime**， **datetime2**，並**smalldatetime**值。 如需詳細資訊，請參閱 <<c0> [ 參數和資料列集的中繼資料](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|IBCPSession::BCPColFmt|如需詳細資訊，請參閱 <<c0> [ 增強型日期和時間類型的大量複製變更&#40;OLE DB&#41;](../../oledb/ole-db-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db.md)。</c0>|  
|ICommandWithParameters::GetParameterInfo|如需詳細資訊，請參閱 <<c0> [ 參數和資料列集的中繼資料](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|ICommandWithParameters::SetParameterinfo|如需詳細資訊，請參閱 <<c0> [ 參數和資料列集的中繼資料](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|IColumnsRowset::GetColumnsRowset|如需詳細資訊，請參閱 <<c0> [ 參數和資料列集的中繼資料](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|IColumnsInfo::GetColumnInfo|如需詳細資訊，請參閱 <<c0> [ 參數和資料列集的中繼資料](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|Idbschemarowset:: Getrowset|如需受影響的結構描述資料列集的詳細資訊，請參閱 <<c0> [ 日期和時間以及結構描述資料列集](../../oledb/ole-db-date-time/metadata-date-and-time-and-schema-rowsets.md)。|  
|IRowsetFastLoad|此介面支援新的日期/時間類型，但是它的介面沒有任何變更。|  
|Itabledefinition:: Createtable|如需詳細資訊，請參閱 < [OLE DB 日期和時間改善的資料型別支援](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)。|  
  
## <a name="see-also"></a>另請參閱  
 [日期和時間改善 &#40;OLE DB&#41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
