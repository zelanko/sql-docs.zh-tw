---
title: OLE DB API 對日期和時間增強功能支援 |Microsoft 文件
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, date/time improvements
ms.assetid: e65c9253-bd99-4dc3-9cb8-7613f754c966
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 2bf7eee4dd2517d4ff9c9f871160ba0515b18ce8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36146278"
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>OLE DB API 對日期和時間增強功能支援
  下列 OLE DB API 支援日期/時間增強功能。  
  
|函數|描述|  
|--------------|-----------------|  
|IAccessor::CreateAccessor|在 DBBINDING 結構中加入一個旗標，好讓應用程式可以區分 `datetime`、`datetime2` 和 `smalldatetime` 值。 如需詳細資訊，請參閱[參數和資料列集的中繼資料](metadata-parameter-and-rowset.md)。|  
|IBCPSession::BCPColFmt|如需詳細資訊，請參閱[增強型日期和時間類型的大量複製變更&#40;OLE DB 和 ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)。|  
|ICommandWithParameters::GetParameterInfo|如需詳細資訊，請參閱[參數和資料列集的中繼資料](metadata-parameter-and-rowset.md)。|  
|ICommandWithParameters::SetParameterinfo|如需詳細資訊，請參閱[參數和資料列集的中繼資料](metadata-parameter-and-rowset.md)。|  
|IColumnsRowset::GetColumnsRowset|如需詳細資訊，請參閱[參數和資料列集的中繼資料](metadata-parameter-and-rowset.md)。|  
|IColumnsInfo::GetColumnInfo|如需詳細資訊，請參閱[參數和資料列集的中繼資料](metadata-parameter-and-rowset.md)。|  
|IDBSchemaRowset::GetRowset|如需受影響的結構描述資料列集的詳細資訊，請參閱[日期和時間以及結構描述資料列集](../native-client-ole-db-rowsets/rowsets.md)。|  
|IRowsetFastLoad|此介面支援新的日期/時間類型，但是它的介面沒有任何變更。|  
|ITableDefinition::CreateTable|如需詳細資訊，請參閱[OLE DB 日期和時間增強功能的資料類型支援](data-type-support-for-ole-db-date-and-time-improvements.md)。|  
  
## <a name="see-also"></a>另請參閱  
 [日期和時間增強功能&#40;OLE DB&#41;](date-and-time-improvements-ole-db.md)  
  
  