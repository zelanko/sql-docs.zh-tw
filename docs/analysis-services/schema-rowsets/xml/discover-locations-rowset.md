---
title: DISCOVER_LOCATIONS 資料列集 |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d65e4ea55f956ce47632cd11a4e6dc5f8cfea377
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="discoverlocations-rowset"></a>DISCOVER_LOCATIONS 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
|**LOCATION_BACKUP_FILE_PATHNAME**|**DBTYPE_WSTR**|必要項|  
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
  
  
