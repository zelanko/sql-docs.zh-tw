---
title: DISCOVER_LOCATIONS 資料列集 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 6d3a1171-8e4d-4022-ade0-b785cf795d70
caps.latest.revision: 7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 90fa167102e9e5a5c8a4ad916bb921205347f1c6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37284434"
---
# <a name="discoverlocations-rowset"></a>DISCOVER_LOCATIONS 資料列集
  傳回備份檔案的內容資訊。 您必須擁有存取備份檔案位置的權限。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `DISCOVER_LOCATIONS`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|限制|描述|  
|-----------------|--------------------|-----------------|-----------------|  
|`LOCATION_BACKUP_FILE_PATHNAME`|`DBTYPE_WSTR`|必要項，請參閱下文。|備份檔案的位置。|  
|`LOCATION_PARTITION_OBJECTPATH`|`DBTYPE_WSTR`||相對於 data 資料夾的資料分割路徑。|  
|`LOCATION_PARTITION_DATASOURCEID`|`DBTYPE_WSTR`||用於處理資料分割的資料來源識別碼。|  
|`LOCATION_PARTITION_DATASOURCENAME`|`DBTYPE_WSTR`||用於處理的資料來源名稱。|  
|`LOCATION_PARTITION_NAME`|`DBTYPE_WSTR`||資料分割名稱。|  
|`LOCATION_PARTITION_SIZE`|`DBTYPE_WSTR`||大約的資料分割大小。|  
|`LOCATION_CONNECTION_STRING`|`DBTYPE_WSTR`||處理中所用之資料來源的連接字串。|  
|`LOCATION_PARTITION_FOLDER`|`DBTYPE_WSTR`||產生備份檔案時此資料分割的原始位置。|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 在下表列出的資料行上可能會限制 `DISCOVER_LOCATIONS` 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|`LOCATION_BACKUP_FILE_PATHNAME`|`DBTYPE_WSTR`|必要項|  
|`LOCATION_PASSWORD PF_DBTYPE`|`DBTYPE_WSTR`|如果在備份期間指定它，則為必要項。 此限制不是用來限制傳回的資料列， 它是用來提供密碼以存取位置。|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 傳回資料列集  
 使用 ADOMD.NET 和結構描述資料列集來擷取中繼資料時，您可以使用 GUID 或字串，在 GetSchemaDataSet 方法中參考結構描述資料列集物件。 如需詳細資訊，請參閱 [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)。  
  
 下表將提供可識別此資料列集的 GUID 和字串值。  
  
|引數|值|  
|--------------|-----------|  
|GUID|a07ccd92-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|位置|  
  
## <a name="see-also"></a>另請參閱  
 [XML for Analysis 結構描述資料列集](xml-for-analysis-schema-rowsets.md)  
  
  
