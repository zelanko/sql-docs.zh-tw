---
title: 針對 OLE DB 資料表值參數而變更的結構描述資料列集 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- schema rowsets [OLE DB]
- table-valued parameters (OLE DB), schema rowsets changed for (OLE DB)
ms.assetid: 581e3ead-53db-44da-8718-f3fc4b5108f1
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d4e7667c06ffea558333cd27f3bfed106cd1a1c9
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2019
ms.locfileid: "73788687"
---
# <a name="schema-rowsets-changed-for-ole-db-table-valued-parameters"></a>針對 OLE DB 資料表值參數而變更的結構描述資料列集
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  下列是已變更或加入來支援資料表值參數的結構描述資料列集。  
  
|結構描述資料列集|描述|  
|-------------------|-----------------|  
|DBSCHEMA_PROCEDURE_PARAMETERS|兩個新的資料行會加在名為 SS_TYPE_CATALOG_NAME 和 SS_TYPE_SCHEMANAME 的資料列集結尾。 這些資料行可以針對未來的類型重複使用。 TYPE_NAME 和 LOCAL_TYPE_NAME 資料行會包含 TABLE 類型的資料表值參數的名稱。 DATA_TYPE 資料行對於資料表值參數具有 DBTYPE_TABLE = 143 值。|  
|DBSCHEMA_TABLE_TYPES|已新增這個資料列集來支援資料表值參數。 這與 DBSCHEMA_TABLES 完全相同，但它只會針對資料表類型 (而不會針對資料表、檢視或同義字) 傳回中繼資料。 TABLE_TYPE 資料行會具有 'TABLE TYPE' 值。|  
|DBSCHEMA_TABLE_TYPE_PRIMARY_KEYS|已新增這個資料列集來支援資料表值參數。 這與 DBSCHEMA_PRIMARY_KEYS 完全相同，但它只會針對資料表類型 (而不會針對資料表) 傳回主索引鍵中繼資料。|  
|DBSCHEMA_TABLE_TYPE_COLUMNS|已新增這個資料列集來支援資料表值參數。 這與 DBSCHEMA_COLUMNS 完全相同，但它只會針對資料表類型 (而不會針對資料表、檢視或同義字) 傳回資料行中繼資料。|  
  
## <a name="see-also"></a>另請參閱  
 [資料表值參數 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [使用資料表值參數 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
