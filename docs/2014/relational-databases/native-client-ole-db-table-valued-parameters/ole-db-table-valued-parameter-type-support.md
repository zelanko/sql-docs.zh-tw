---
title: OLE DB 資料表值參數類型支援 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (OLE DB), API support (OLE DB)
ms.assetid: 147036a0-260e-4f81-8b3b-89209e023a32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 27ae90e05784c18d85f84daa9955818d3133ad07
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63046502"
---
# <a name="ole-db-table-valued-parameter-type-support"></a>OLE DB 資料表值參數類型支援
  本主題描述資料表值參數的 OLE DB 類型支援。  
  
## <a name="table-valued-parameter-rowset-object"></a>資料表值參數資料列集物件  
 您可以針對資料表值參數建立專用的資料列集物件。 您可以使用 ITableDefinitionWithConstraints::CreateTableWithConstraints 或 iopenrowset:: Openrowset，以建立資料表值參數資料列集物件。 若要這樣做，請將 *pTableID* 參數的 *eKind* 成員設定為 DBKIND_GUID_NAME，並提供 CLSID_ROWSET_INMEMORY 當作 *guid* 成員。 資料表值參數的伺服器類型名稱必須指定在*pwszName*隸屬*pTableID*使用 iopenrowset:: Openrowset 時。 資料表值參數資料列集物件的行為就如同一般 SQL Server Native Client OLE DB 提供者物件。  
  
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
  
 DBTYPE_TABLE 與 DBTYPE_IUNKNOWN 具有相同的格式。 它是資料緩衝區中物件的指標。 若為繫結中的完整規格，取用者會填滿 DBOBJECT 緩衝區，並將 *iid* 設定為其中一個資料列集物件介面 (IID_IRowset)。 如果繫結中沒有指定任何 DBOBJECT，系統就會採用 IID_IRowset。  
  
 不支援針對任何其他類型在 DBTYPE_TABLE 之間來回轉換。 IConvertType::CanConvert 會針對任何要求的不支援轉換傳回 S_FALSE，但 DBTYPE_TABLE 與 DBTYPE_TABLE 的轉換除外。 這會採用 Command 物件的 DBCONVERTFLAGS_PARAMETER。  
  
## <a name="methods"></a>方法  
 如需 OLE DB 方法支援資料表值參數的資訊，請參閱[OLE DB Table-Valued 參數類型支援&#40;方法&#41;](ole-db-table-valued-parameter-type-support-methods.md)。  
  
## <a name="properties"></a>屬性  
 OLE DB 屬性支援資料表值參數的相關資訊，請參閱[OLE DB Table-Valued 參數類型支援&#40;屬性&#41;](ole-db-table-valued-parameter-type-support-properties.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料表值參數 &#40;OLE DB&#41;](table-valued-parameters-ole-db.md)   
 [使用資料表值參數 &#40;OLE DB&#41;](../native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
