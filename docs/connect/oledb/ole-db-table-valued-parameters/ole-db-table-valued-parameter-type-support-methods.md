---
title: OLE DB 資料表值參數類型支援 (方法) | Microsoft Docs
description: OLE DB 資料表值參數類型支援 (方法)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (OLE DB), API support (methods)
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: dfa166cb07e1aae53426f48027eb539bca9f60ad
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43017668"
---
# <a name="ole-db-table-valued-parameter-type-support-methods"></a>OLE DB 資料表值參數類型支援 (方法)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  下列標準 OLE DB 方法支援資料表值參數：  
  
|方法|資料表值參數支援|  
|------------|-------------------------------------|  
|ITableDefinitionWithConstraints::CreateTableWithConstraints|當您知道資料表值參數的類型資訊，而且想要根據類型資訊來具現化資料表值參數資料列集物件時使用。<br /><br /> 如需詳細資訊，請參閱 < 靜態案例 > 中[資料表值參數資料列集建立](../../oledb/ole-db-table-valued-parameters/table-valued-parameter-rowset-creation.md)。|  
|IOpenRowset::OpenRowset|當您不知道資料表值參數的類型資訊，而且想要根據從伺服器擷取的中繼資料資訊來具現化資料表值參數資料列集物件時使用。<br /><br /> 如需詳細資訊，請參閱 < 動態案例 > 中[資料表值參數資料列集建立](../../oledb/ole-db-table-valued-parameters/table-valued-parameter-rowset-creation.md)。|  
|ISSCommandWithParameters::SetParameterInfo|若要指定資料表值參數命令參數，取用者會在 DBPARAMBINDINFO 結構的 *pwszName* 成員中將此參數的類型指定為 "table" 或 "DBTYPE_TABLE"。 *UlParamSize*設定為 ~ 0。 如需詳細資訊，請參閱 「 資料表值參數規格 」 中[Executing Commands Containing Table-Valued 參數](../../oledb/ole-db-table-valued-parameters/executing-commands-containing-table-valued-parameters.md)。|  
|ISSCommandWithParameters::SetParameterProperties|會設定資料表值參數所特有的屬性，例如結構描述名稱、類型名稱、資料行順序和預設資料行。<br /><br /> 取用者會在 SSPARAMPROPS 結構的 *iOrdinal* 中指定參數的序數。 所要求的屬性集為 DBPROPSET_SQLSERVERPARAMETER。|  
|ISSCommandWithParameters::GetParameterInfo|取得指定之命令的所有參數類型。<br /><br /> 如果是資料表值參數，DBPARAMINFO 結構中的 *wType* 欄位將會具有 DBTYPE_TABLE 類型。 *ulParamSize* 欄位將會設定為 ~0，表示長度未知。|  
|ISSCommandWithParameters::GetParameterProperties|取得 DBTYPE_TABLE 類型之參數的其他類型資訊。<br /><br /> 取用者會在 SSPARAMPROPS 結構的 *iOrdinal* 成員中指定參數的序數。 取用者可以要求任何列在 isscommandwithparameters:: Setparameterproperties DBPROPSET_SQLSERVERPARAMETER 屬性集裡的屬性。<br /><br /> 因為取用者不知道資料表值參數類型，所以提供者必須將 SSPROP_PARAM_TYPE_TYPENAME、SSPROP_PARAM_TYPE_SCHEMANAME 和 SSPROP_PARAM_TYPE_CATALOGNAME 設定為正確的值。 其餘的 SSPROP_PARAM_TABLE_DEFAULT_COLUMNS 和 SSPROP_PARAM_TABLE_COLUMN_SORT_ORDER 屬性將會有預設值。 當取用者已經探索出資料表值參數類型名稱時，它會使用 IOpenRowset::OpenRowset 來建立這個資料表值參數的執行個體，並指定資料表值參數類型的名稱。 如需詳細資訊，請參閱 <<c0> [ 資料表值參數類型探索](../../oledb/ole-db-table-valued-parameters/table-valued-parameter-type-discovery.md)。|  
|Irowsetinfo:: Getproperties|取得資料表值參數資料列集屬性。 取用者可以使用這些屬性，以最佳方式設定繫結。|  
|IColumnsRowset::GetColumnsRowset|擷取有關 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料表的中繼資料資訊。 如果是資料表值參數，這個相同介面會提供有關每一個資料行的詳細中繼資料資訊，如下所示：<br /><br /> DBCOLUMN_FLAGS 表示透過 DBCOLUMNFLAGS_ISNULLABLE 位元的 Null 屬性。<br /><br /> DBCOLUMN_ISUNIQUE 會指出此資料行是否為識別欄位。<br /><br /> DBCOLUMN_COMPUTEMODE 會指出此資料行是否為計算資料行。|  
|Iaccessor:: Createaccessor|若要將資料表值參數資料列集物件繫結到命令參數，當您建立存取子時，請將它的 *wType* 成員設定為 DBTYPE_TABLE。 DBOBJECT 結構將會包含 IID_IRowset 或是 *iid* 成員中任何其他有效的資料列集物件介面。 其餘欄位的處理方式類似於 DBTYPE_IUNKNOWN。|  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB 資料表值參數類型支援](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support.md)   
 [建立資料表值參數資料列集](../../oledb/ole-db-table-valued-parameters/table-valued-parameter-rowset-creation.md)   
 [使用資料表值參數 &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
