---
title: 資料來源資訊屬性 |Microsoft Docs
description: 資料來源資訊屬性
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- information properties [OLE DB]
- OLE DB data source properties [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: ab8c77e44c5ed8646e3ffb1f80718d618c234b39
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47600161"
---
# <a name="data-source-information-properties"></a>資料來源資訊屬性
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  在提供者特定的屬性集 DBPROPSET_SQLSERVERDATASOURCEINFO 中，OLE DB Driver for SQL Server 會定義下列資料來源資訊屬性。  
  
|屬性識別碼|Description|  
|-----------------|-----------------|  
|SSPROP_COLUMNLEVELCOLLATION|類型：VT_BOOL<br /><br /> R/W：讀取<br /><br /> 預設值：VARIANT_TRUE<br /><br /> 描述：用於判斷是否支援資料行定序。<br /><br /> VARIANT_TRUE：支援資料行層級定序。<br /><br /> VARIANT_FALSE：不支援資料行層級定序。|  
|SSPROP_UNICODELCID|類型：VT_I4 R/W：讀取<br /><br /> 描述：Unicode 地區設定識別碼。<br /><br /> 這是用於 Unicode 資料排序的地區設定。|  
|SSPROP_UNICODECOMPARISONSTYLE|類型：VT_I4 R/W：讀取<br /><br /> 描述：Unicode 比較樣式。<br /><br /> 用於 Unicode 資料排序的排序選項。|  
  
 在提供者特定的屬性集 DBPROPSET_SQLSERVERSTREAM 中，OLE DB Driver for SQL Server 會定義下列其他屬性。  
  
|屬性識別碼|Description|  
|-----------------|-----------------|  
|SSPROP_STREAM_XMLROOT|類型：VT_BSTR R/W：讀取/寫入<br /><br /> 描述：FOR XML 查詢的結果可能不是格式正確的文件。 指定這個屬性時，結果 ' 選取... for XML' 查詢會包裝在這個屬性，以傳回格式正確的 XML 文件所提供的根標記。 如果在瀏覽器中執行查詢，載入結果時，它可能會使瀏覽器顯示剖析器錯誤。 為避免這個錯誤，SQL ISAPI 支援關鍵字 ROOT。 此關鍵字會對應至 SSPROP_STREAM_XMLROOT 屬性。|  
  
## <a name="see-also"></a>另請參閱  
 [資料來源物件&#40;OLE DB&#41;](../../oledb/ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
