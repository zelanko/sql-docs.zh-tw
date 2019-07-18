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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ef6334f6fe4671f2563add857f6dd58ce67a2840
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63237841"
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>OLE DB API 對日期和時間增強功能的支援
  下列 OLE DB API 支援日期/時間增強功能。  
  
|函數|描述|  
|--------------|-----------------|  
|IAccessor::CreateAccessor|在 DBBINDING 結構中加入一個旗標，好讓應用程式可以區分 `datetime`、`datetime2` 和 `smalldatetime` 值。 如需詳細資訊，請參閱 <<c0> [ 參數和資料列集的中繼資料](metadata-parameter-and-rowset.md)。|  
|IBCPSession::BCPColFmt|如需詳細資訊，請參閱 <<c0> [ 增強型日期和時間類型的大量複製變更&#40;OLE DB 和 ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)。</c0>|  
|ICommandWithParameters::GetParameterInfo|如需詳細資訊，請參閱 <<c0> [ 參數和資料列集的中繼資料](metadata-parameter-and-rowset.md)。|  
|ICommandWithParameters::SetParameterinfo|如需詳細資訊，請參閱 <<c0> [ 參數和資料列集的中繼資料](metadata-parameter-and-rowset.md)。|  
|IColumnsRowset::GetColumnsRowset|如需詳細資訊，請參閱 <<c0> [ 參數和資料列集的中繼資料](metadata-parameter-and-rowset.md)。|  
|IColumnsInfo::GetColumnInfo|如需詳細資訊，請參閱 <<c0> [ 參數和資料列集的中繼資料](metadata-parameter-and-rowset.md)。|  
|IDBSchemaRowset::GetRowset|如需受影響的結構描述資料列集的詳細資訊，請參閱 <<c0> [ 日期和時間以及結構描述資料列集](../native-client-ole-db-rowsets/rowsets.md)。|  
|IRowsetFastLoad|此介面支援新的日期/時間類型，但是它的介面沒有任何變更。|  
|ITableDefinition::CreateTable|如需詳細資訊，請參閱 < [OLE DB 日期和時間改善的資料型別支援](data-type-support-for-ole-db-date-and-time-improvements.md)。|  
  
## <a name="see-also"></a>另請參閱  
 [日期和時間改善 &#40;OLE DB&#41;](date-and-time-improvements-ole-db.md)  
  
  
