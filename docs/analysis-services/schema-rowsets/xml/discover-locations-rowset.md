---
title: "DISCOVER_LOCATIONS 資料列集 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 6d3a1171-8e4d-4022-ade0-b785cf795d70
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 15828ba16158f97479010617a68a5f3a11cf185e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="discoverlocations-rowset"></a>DISCOVER_LOCATIONS 資料列集
  傳回備份檔案的內容資訊。 您必須擁有存取備份檔案位置的權限。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DISCOVER_LOCATIONS**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|限制|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**LOCATION_BACKUP_FILE_PATHNAME**|**DBTYPE_WSTR**|必要項，請參閱下文。|備份檔案的位置。|  
|**LOCATION_PARTITION_OBJECTPATH**|**DBTYPE_WSTR**||相對於 data 資料夾的資料分割路徑。|  
|**LOCATION_PARTITION_DATASOURCEID**|**DBTYPE_WSTR**||用於處理資料分割的資料來源識別碼。|  
|**LOCATION_PARTITION_DATASOURCENAME**|**DBTYPE_WSTR**||用於處理的資料來源名稱。|  
|**LOCATION_PARTITION_NAME**|**DBTYPE_WSTR**||資料分割名稱。|  
|**LOCATION_PARTITION_SIZE**|**DBTYPE_WSTR**||大約的資料分割大小。|  
|**LOCATION_CONNECTION_STRING**|**DBTYPE_WSTR**||處理中所用之資料來源的連接字串。|  
|**LOCATION_PARTITION_FOLDER**|**DBTYPE_WSTR**||產生備份檔案時此資料分割的原始位置。|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 **DISCOVER_LOCATIONS**上表中列出的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**LOCATION_BACKUP_FILE_PATHNAME**|**DBTYPE_WSTR**|Required|  
|**LOCATION_PASSWORD PF_DBTYPE**|**DBTYPE_WSTR**|如果在備份期間指定它，則為必要項。 此限制不是用來限制傳回的資料列， 它是用來提供密碼以存取位置。|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 傳回資料列集  
 使用 ADOMD.NET 和結構描述資料列集來擷取中繼資料時，您可以使用 GUID 或字串，在 GetSchemaDataSet 方法中參考結構描述資料列集物件。 如需詳細資訊，請參閱 [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)。  
  
 下表將提供可識別此資料列集的 GUID 和字串值。  
  
|引數|值|  
|--------------|-----------|  
|GUID|a07ccd92-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|位置|  
  
## <a name="see-also"></a>另請參閱  
 [XML for Analysis 結構描述資料列集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  

