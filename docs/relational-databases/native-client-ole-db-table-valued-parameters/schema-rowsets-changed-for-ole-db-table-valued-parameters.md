---
description: 變更 SQL Server Native Client 中 OLE DB 資料表值參數的架構資料列集
title: 架構資料列集，OLE DB 資料表值參數
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d68366d87fdee64096ebca492b318c711fd2b038
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482594"
---
# <a name="schema-rowsets-changed-for-ole-db-table-valued-parameters-in-sql-server-native-client"></a>變更 SQL Server Native Client 中 OLE DB 資料表值參數的架構資料列集
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  下列是已變更或加入來支援資料表值參數的結構描述資料列集。  
  
|結構描述資料列集|描述|  
|-------------------|-----------------|  
|DBSCHEMA_PROCEDURE_PARAMETERS|兩個新的資料行會加在名為 SS_TYPE_CATALOG_NAME 和 SS_TYPE_SCHEMANAME 的資料列集結尾。 這些資料行可以針對未來的類型重複使用。 TYPE_NAME 和 LOCAL_TYPE_NAME 資料行會包含 TABLE 類型的資料表值參數的名稱。 DATA_TYPE 資料行對於資料表值參數具有 DBTYPE_TABLE = 143 值。|  
|DBSCHEMA_TABLE_TYPES|已新增這個資料列集來支援資料表值參數。 這與 DBSCHEMA_TABLES 完全相同，但它只會針對資料表類型 (而不會針對資料表、檢視或同義字) 傳回中繼資料。 TABLE_TYPE 資料行會具有 'TABLE TYPE' 值。|  
|DBSCHEMA_TABLE_TYPE_PRIMARY_KEYS|已新增這個資料列集來支援資料表值參數。 這與 DBSCHEMA_PRIMARY_KEYS 完全相同，但它只會針對資料表類型 (而不會針對資料表) 傳回主索引鍵中繼資料。|  
|DBSCHEMA_TABLE_TYPE_COLUMNS|已新增這個資料列集來支援資料表值參數。 這與 DBSCHEMA_COLUMNS 完全相同，但它只會針對資料表類型 (而不會針對資料表、檢視或同義字) 傳回資料行中繼資料。|  
|||

## <a name="see-also"></a>另請參閱  
 [資料表值參數 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [使用資料表值參數 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
