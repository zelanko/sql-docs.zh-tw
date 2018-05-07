---
title: OLE DB 資料表值參數類型支援 |Microsoft 文件
description: OLE DB Table-Valued 參數類型支援
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (OLE DB), API support (OLE DB)
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 8f1a20a09e4c15b0dbe84352a4bfbbef59b5d784
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="ole-db-table-valued-parameter-type-support"></a>OLE DB 資料表值參數類型支援
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本文描述針對資料表值參數的 OLE DB 類型支援。  
  
## <a name="table-valued-parameter-rowset-object"></a>資料表值參數資料列集物件  
 您可以針對資料表值參數建立專用的資料列集物件。 您使用 ITableDefinitionWithConstraints::CreateTableWithConstraints 或 iopenrowset:: Openrowset 建立資料表值參數資料列集物件。 若要這樣做，請設定*eKind*隸屬*Createtable*參數為 DBKIND_GUID_NAME，並提供 CLSID_ROWSET_INMEMORY 當做*guid*成員。 必須指定資料表值參數的伺服器類型名稱中*pwszName*隸屬*Createtable*使用 iopenrowset:: Openrowset 時。 資料表值參數資料列集物件的行為就像一般 OLE DB 驅動程式的 SQL Server 物件。  
  
```  
const GUID CLSID_ROWSET_TVP =   
{0xc7ef28d5, 0x7bee, 0x443f, {0x86, 0xda, 0xe3, 0x98, 0x4f, 0xcd, 0x4d, 0xf9}};  
  
CoType RowsetTVP  
{  
[mandatory] interface IAccessor;  
[mandatory] interface IColumnsInfo;  
[mandatory] interface IConvertType;  
[mandatory] interface IRowset;  
[mandatory] interface IRowsetInfo;  
[optional]  interface IColumnsRowset;  
[optional]  interface IRowsetChange;  
[optional]  interface ISupportErrorInfo;  
};  
```  
  
## <a name="dbtypetable"></a>DBTYPE_TABLE  
 新的類型 DBTYPE_TABLE 代表資料表類型。 這個類型會在需要 DBTYPE 的各種 OLE DB 介面中指定資料表值參數。  
  
```  
#define DBTYPE_TABLE (143)  
```  
  
 DBTYPE_TABLE 與 DBTYPE_IUNKNOWN 具有相同的格式。 這是資料緩衝區中的物件指標。 繫結中的完整規格，取用者會填滿 DBOBJECT 緩衝區，與*iid*設為其中一個資料列集物件介面 (IID_IRowset)。 如果繫結中不指定任何 DBOBJECT，則會假設 IID_IRowset。  
  
 不支援轉換 dbtype_table 之間來回的任何其他類型。 IConvertType::CanConvert 會針對任何要求 dbtype_table 與 DBTYPE_TABLE 的轉換不支援轉換傳回 S_FALSE。 這會假設命令物件的 DBCONVERTFLAGS_PARAMETER。  
  
## <a name="methods"></a>方法  
 有關 OLE DB 方法支援資料表值參數的詳細資訊，請參閱[OLE DB Table-Valued 參數類型支援&#40;方法&#41;](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-methods.md)。  
  
## <a name="properties"></a>屬性  
 OLE DB 屬性支援資料表值參數的相關資訊，請參閱[OLE DB Table-Valued 參數類型支援&#40;屬性&#41;](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-properties.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料表值參數&#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [使用資料表值參數 & #40; OLE DB & #41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
