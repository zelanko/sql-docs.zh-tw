---
title: OLE DB API 對日期和時間增強功能的支援 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, date/time improvements
ms.assetid: e65c9253-bd99-4dc3-9cb8-7613f754c966
author: rothja
ms.author: jroth
ms.openlocfilehash: cdb17f0d2104373ea797ff9403cc417dfaa3d868
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85056256"
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>OLE DB API 對日期和時間增強功能的支援
  下列 OLE DB API 支援日期/時間增強功能。  
  
|函式|描述|  
|--------------|-----------------|  
|IAccessor::CreateAccessor|在 DBBINDING 結構中加入一個旗標，好讓應用程式可以區分 `datetime`、`datetime2` 和 `smalldatetime` 值。 如需詳細資訊，請參閱[參數和資料列集中繼資料](metadata-parameter-and-rowset.md)。|  
|IBCPSession::BCPColFmt|如需詳細資訊，請參閱[增強型日期和時間類型的大量複製變更 &#40;OLE DB 和 ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)。|  
|ICommandWithParameters::GetParameterInfo|如需詳細資訊，請參閱[參數和資料列集中繼資料](metadata-parameter-and-rowset.md)。|  
|ICommandWithParameters::SetParameterinfo|如需詳細資訊，請參閱[參數和資料列集中繼資料](metadata-parameter-and-rowset.md)。|  
|IColumnsRowset::GetColumnsRowset|如需詳細資訊，請參閱[參數和資料列集中繼資料](metadata-parameter-and-rowset.md)。|  
|IColumnsInfo::GetColumnInfo|如需詳細資訊，請參閱[參數和資料列集中繼資料](metadata-parameter-and-rowset.md)。|  
|IDBSchemaRowset::GetRowset|如需受影響結構描述資料列集的詳細資訊，請參閱[日期和時間以及結構描述資料列集](../native-client-ole-db-rowsets/rowsets.md)。|  
|IRowsetFastLoad|此介面支援新的日期/時間類型，但是它的介面沒有任何變更。|  
|ITableDefinition::CreateTable|如需詳細資訊，請參閱[對 OLE DB 日期和時間改善的資料類型支援](data-type-support-for-ole-db-date-and-time-improvements.md)。|  
  
## <a name="see-also"></a>另請參閱  
 [日期和時間改善 &#40;OLE DB&#41;](date-and-time-improvements-ole-db.md)  
  
  
