---
title: OLE DB API 對日期和時間增強功能的支援 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: e65c9253-bd99-4dc3-9cb8-7613f754c966
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9f99055c13cf04f15d652f79258b10654410e98c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909238"
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>OLE DB API 對日期和時間增強功能的支援
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  下列 OLE DB API 支援日期/時間增強功能。  
  
|函數|描述|  
|--------------|-----------------|  
|IAccessor::CreateAccessor|若要啟用應用程式可以區分 DBBINDING 結構中加入旗標**datetime**， **datetime2**，並**smalldatetime**值。 如需詳細資訊，請參閱 <<c0> [ 參數和資料列集的中繼資料](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|IBCPSession::BCPColFmt|如需詳細資訊，請參閱 <<c0> [ 增強型日期和時間類型的大量複製變更&#40;OLE DB 和 ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)。</c0>|  
|ICommandWithParameters::GetParameterInfo|如需詳細資訊，請參閱 <<c0> [ 參數和資料列集的中繼資料](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|ICommandWithParameters::SetParameterinfo|如需詳細資訊，請參閱 <<c0> [ 參數和資料列集的中繼資料](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|IColumnsRowset::GetColumnsRowset|如需詳細資訊，請參閱 <<c0> [ 參數和資料列集的中繼資料](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|IColumnsInfo::GetColumnInfo|如需詳細資訊，請參閱 <<c0> [ 參數和資料列集的中繼資料](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|IDBSchemaRowset::GetRowset|如需受影響的結構描述資料列集的詳細資訊，請參閱 <<c0> [ 日期和時間以及結構描述資料列集](../../relational-databases/native-client-ole-db-date-time/metadata-date-and-time-and-schema-rowsets.md)。|  
|IRowsetFastLoad|此介面支援新的日期/時間類型，但是它的介面沒有任何變更。|  
|ITableDefinition::CreateTable|如需詳細資訊，請參閱 < [OLE DB 日期和時間改善的資料型別支援](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)。|  
  
## <a name="see-also"></a>另請參閱  
 [日期和時間改善 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
