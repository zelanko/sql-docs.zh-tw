---
title: "DBSCHEMA_COLUMNS 資料列集 |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DBSCHEMA_COLUMNS
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DBSCHEMA_COLUMNS rowset
ms.assetid: 653bdd07-a533-4a99-8b6a-6e5c7322e1f3
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 32df882f6f6b34c4cd5049713240460c62324ddb
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="dbschemacolumns-rowset"></a>DBSCHEMA_COLUMNS 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]提供符合提供之限制準則的所有資料行的資料行資訊。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DBSCHEMA_COLUMNS**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|**TABLE_CATALOG 排列**|**DBTYPE_WSTR**||資料庫的名稱。|  
|**TABLE_SCHEMA**|**DBTYPE_WSTR**||不支援。|  
|**TABLE_NAME**|**DBTYPE_WSTR**||Cube 的名稱。|  
|**COLUMN_NAME**|**DBTYPE_WSTR**||屬性階層或量值的名稱。|  
|**COLUMN_GUID**|**DBTYPE_GUID**||不支援。|  
|**COLUMN_PROPID**|**DBTYPE_UI4**||不支援。|  
|**ORDINAL_POSITION**|**DBTYPE_UI4**||以 1 為開頭的資料行位置。|  
|**COLUMN_HAS_DEFAULT**|**DBTYPE_BOOL**||不支援。|  
|**COLUMN_DEFAULT**|**DBTYPE_WSTR**||不支援。|  
|**COLUMN_FLAGS**|**DBTYPE_UI4**||A **DBCOLUMNFLAGS**位元遮罩，指出資料行屬性。 請參閱 'DBCOLUMNFLAGS 列舉型別' [icolumnsinfo:: Getcolumninfo](http://msdn2.microsoft.com/library/ms722704.aspx)|  
|**IS_NULLABLE**|**DBTYPE_BOOL**||一律傳回**false**。|  
|**DATA_TYPE**|**DBTYPE_WSTR**<br /><br /> **DBTYPE_VARIANT**||資料行的資料類型。 傳回維度資料行的字串以及量值的變數。|  
|**TYPE_GUID**|**DBTYPE_GUID**||不支援。|  
|**CHARACTER_MAXIMUM_LENGTH**|**DBTYPE_UI4**||資料行中值的最大可能長度。<br /><br /> 這擷取自**DataSize**屬性**DataItem**。|  
|**CHARACTER_OCTET_LENGTH**|**DBTYPE_UI4**||針對字元或是二進位資料行，資料行中值的最大可能長度 (以位元組為單位)。<br /><br /> 值為零 (0) 表示資料行沒有最大長度限制。<br /><br /> **NULL**將不會傳回二進位或字元資料類型的資料行傳回。|  
|**NUMERIC_PRECISION**|**DBTYPE_UI2**||最大的有效位數的數值資料的資料行以外的類型**DBTYPE_VARNUMERIC**。|  
|**NUMERIC_SCALE**|**DBTYPE_I2**||小數點右邊的位數**DBTYPE_DECIMAL**， **DBTYPE_NUMERIC**， **DBTYPE_VARNUMERIC**。 否則，這是**NULL**。|  
|**DATETIME_PRECISION**|**DBTYPE_UI4**||不支援。|  
|**CHARACTER_SET_CATALOG**|**DBTYPE_WSTR**||不支援。|  
|**CHARACTER_SET_SCHEMA**|**DBTYPE_WSTR**||不支援。|  
|**CHARACTER_SET_NAME**|**DBTYPE_WSTR**||不支援。|  
|**COLLATION_CATALOG**|**DBTYPE_WSTR**||不支援。|  
|**COLLATION_SCHEMA**|**DBTYPE_WSTR**||不支援。|  
|**SYS.DATABASES**|**DBTYPE_WSTR**||不支援。|  
|**DOMAIN_CATALOG**|**DBTYPE_WSTR**||不支援。|  
|**DOMAIN_SCHEMA**|**DBTYPE_WSTR**||不支援。|  
|**網域名稱**|**DBTYPE_WSTR**||不支援。|  
|**DESCRIPTION**|**DBTYPE_WSTR**||不支援。|  
|**COLUMN_OLAP_TYPE**|**DBTYPE_WSTR**||物件的 OLAP 類型。<br /><br /> **量值**指出物件是量值。<br /><br /> **屬性**指出物件是維度屬性。<br /><br /> **結構描述**指出物件為結構描述中的資料行。|  
  
 排序資料列集**table_catalog 排列**， **TABLE_SCHEMA**， **TABLE_NAME**。  
  
## <a name="restriction-columns"></a>限制資料行  
 **DBSCHEMA_COLUMNS**上表中列出的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**TABLE_CATALOG 排列**|**DBTYPE_WSTR**|選擇性|  
|**TABLE_SCHEMA**|**DBTYPE_WSTR**|選擇性|  
|**TABLE_NAME**|**DBTYPE_WSTR**|選擇性|  
|**COLUMN_NAME**|**DBTYPE_WSTR**|選擇性|  
|**COLUMN_OLAP_TYPE**|**DBTYPE_WSTR**|選擇性|  
  
## <a name="see-also"></a>請參閱  
 [OLE DB 結構描述資料列集](../../../analysis-services/schema-rowsets/ole-db/ole-db-schema-rowsets.md)  
  
  
