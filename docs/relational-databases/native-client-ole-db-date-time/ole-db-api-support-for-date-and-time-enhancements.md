---
title: "OLE DB API 對日期和時間增強功能支援 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-date-time
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: e65c9253-bd99-4dc3-9cb8-7613f754c966
caps.latest.revision: "10"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4f33b6aa10205aa13203384a39201642f94c5a4b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>OLE DB API 對日期和時間增強功能支援
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  下列 OLE DB API 支援日期/時間增強功能。  
  
|函數|Description|  
|--------------|-----------------|  
|Iaccessor:: Createaccessor|若要啟用應用程式可以區分 DBBINDING 結構中加入旗標**datetime**， **datetime2**，和**smalldatetime**值。 如需詳細資訊，請參閱[參數和資料列集的中繼資料](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|Ibcpsession:: Bcpcolfmt|如需詳細資訊，請參閱[增強型日期和時間類型 &#40; OLE DB 和 ODBC &#41; 的大量複製變更](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)。|  
|ICommandWithParameters::GetParameterInfo|如需詳細資訊，請參閱[參數和資料列集的中繼資料](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|Icommandwithparameters:: Setparameterinfo|如需詳細資訊，請參閱[參數和資料列集的中繼資料](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|IColumnsRowset::GetColumnsRowset|如需詳細資訊，請參閱[參數和資料列集的中繼資料](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|IColumnsInfo::GetColumnInfo|如需詳細資訊，請參閱[參數和資料列集的中繼資料](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md)。|  
|Idbschemarowset:: Getrowset|如需受影響的結構描述資料列集的詳細資訊，請參閱[日期和時間以及結構描述資料列集](../../relational-databases/native-client-ole-db-date-time/metadata-date-and-time-and-schema-rowsets.md)。|  
|IRowsetFastLoad|此介面支援新的日期/時間類型，但是它的介面沒有任何變更。|  
|Itabledefinition:: Createtable|如需詳細資訊，請參閱[OLE DB 日期和時間增強功能的資料類型支援](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)。|  
  
## <a name="see-also"></a>請參閱＜  
 [日期和時間增強功能 &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
