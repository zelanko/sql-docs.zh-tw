---
title: OLE DB 資料表值參數類型支援 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (OLE DB), API support (OLE DB)
ms.assetid: 147036a0-260e-4f81-8b3b-89209e023a32
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 4b6416715cc6226766773d3f1d630dc2e42e1e37
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36131473"
---
# <a name="ole-db-table-valued-parameter-type-support"></a>OLE DB 資料表值參數類型支援
  本主題描述資料表值參數的 OLE DB 類型支援。  
  
## <a name="table-valued-parameter-rowset-object"></a>資料表值參數資料列集物件  
 您可以針對資料表值參數建立專用的資料列集物件。 您使用 ITableDefinitionWithConstraints::CreateTableWithConstraints 或 iopenrowset:: Openrowset 建立資料表值參數資料列集物件。 若要這樣做，請設定*eKind*隸屬*Createtable*參數為 DBKIND_GUID_NAME，並提供 CLSID_ROWSET_INMEMORY 當做*guid*成員。 必須指定資料表值參數的伺服器類型名稱中*pwszName*隸屬*Createtable*使用 iopenrowset:: Openrowset 時。 資料表值參數資料列集物件的行為就如同一般 SQL Server Native Client OLE DB 提供者物件。  
  
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
  
 DBTYPE_TABLE 與 DBTYPE_IUNKNOWN 具有相同的格式。 它是資料緩衝區中物件的指標。 繫結中的完整規格，取用者會填滿 DBOBJECT 緩衝區，與*iid*設為其中一個資料列集物件介面 (IID_IRowset)。 如果繫結中不指定任何 DBOBJECT，則會假設 IID_IRowset。  
  
 不支援針對任何其他類型在 DBTYPE_TABLE 之間來回轉換。 IConvertType::CanConvert 會針對任何要求 dbtype_table 與 DBTYPE_TABLE 的轉換不支援轉換傳回 S_FALSE。 這會假設命令物件的 DBCONVERTFLAGS_PARAMETER。  
  
## <a name="methods"></a>方法  
 有關 OLE DB 方法支援資料表值參數的詳細資訊，請參閱[OLE DB Table-Valued 參數類型支援&#40;方法&#41;](ole-db-table-valued-parameter-type-support-methods.md)。  
  
## <a name="properties"></a>屬性  
 如需 infornation 有關支援資料表值參數的 OLE DB 屬性，請參閱[OLE DB Table-Valued 參數類型支援&#40;屬性&#41;](ole-db-table-valued-parameter-type-support-properties.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料表值參數&#40;OLE DB&#41;](table-valued-parameters-ole-db.md)   
 [您可以使用資料表值參數&#40;OLE DB&#41;](../native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  