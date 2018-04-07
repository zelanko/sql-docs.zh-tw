---
title: OLE DB 資料表值參數類型支援 （屬性） |Microsoft 文件
description: OLE DB Table-Valued 參數類型支援 （屬性）
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (OLE DB), API support (properties)
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fd92ddcac9238e30993b59ad004676572878fd04
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2018
---
# <a name="ole-db-table-valued-parameter-type-support-properties"></a>OLE DB 資料表值參數類型支援 (屬性)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本主題提供與資料表值參數資料列集物件相關聯之 OLE DB 屬性和屬性集的相關資訊。  
  
## <a name="properties"></a>屬性  
 以下是透過 IRowsetInfo::GetPropeties 方法在資料表值參數資料列集物件上公開的屬性清單。 請注意，所有資料表值參數資料列集屬性都是唯讀的。 因此，嘗試設定任何透過 iopenrowset:: Openrowset 或 ITableDefinitionWithConstraints::CreateTableWithConstraints 屬性的方法為非預設值會導致錯誤，而且會建立任何物件。  
  
 沒有在資料表值參數資料列集物件中實作的屬性不會列在此處。 如需屬性的完整清單，請參閱 OLE DB 文件集中的＜Windows Data Access Components＞。  
  
|屬性識別碼|Value|  
|-----------------|-----------|  
|DBPROP_ABORTPRESERVE|VARIANT_TRUE|  
|DBPROP_ACCESSORDER|DBPROPVAL_AO_RANDOM|  
|DBPROP_BLOCKINGSTORAGEOBJECTS|VARIANT_TRUE|  
|DBPROP_BOOKMARKS<br /><br /> DBPROP_LITERALBOOKMARKS|R/W：唯讀<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述：在資料表值參數資料列集物件上不允許使用書籤。|  
|DBPROP_BOOKMARKSKIPPED|VARIANT_FALSE|  
|DBPROP_BOOKMARKTYPE|DBPROPVAL_BMK_NUMERIC|  
|DBPROP_CANHOLDROWS|VARIANT_FALSE|  
|DBPROP_CHANGEINSERTEDROWS|VARIANT_TRUE|  
|DBPROP_COLUMNRESTRICT|VARIANT_FALSE|  
|DBPROP_COMMANDTIMEOUT|0|  
|DBPROP_COMMITPRESERVE|VARIANT_TRUE|  
|DBPROP_DEFERRED|VARIANT_FALSE|  
|DBPROP_DELAYSTORAGEOBJECTS|VARIANT_FALSE|  
|DBPROP_IAccessor<br /><br /> DBPROP_IColumnsInfo<br /><br /> DBPROP_IConvertType<br /><br /> DBPROP_IRowset<br /><br /> DBPROP_IRowsetInfo<br /><br /> DBPROP_IColumnsRowset|VARIANT_TRUE|  
|DBPROP_IConnectionPointContainer<br /><br /> DBPROP_IMultipleResults<br /><br /> DBPROP_IRowsetUpdate<br /><br /> DBPROP_IRowsetIdentity<br /><br /> DBPROP_IRowsetLocate<br /><br /> DBPROP_IRowsetScroll<br /><br /> DBPROP_IRowsetResynch|VARIANT_FALSE|  
|DBPROP_IRowsetChange|VARIANT_TRUE<br /><br /> 注意： 資料表值參數資料列集物件支援的 IRowsetChange 介面。<br /><br /> 使用 DBPROP_IRowsetChange 等於 VARIANT_TRUE 建立的資料列集會表現立即更新模式行為。<br /><br /> 不過，如果為 ISequentialStream 物件繫結 BLOB 資料行，取用者必須將它們保留資料表值參數資料列集物件的存留期。|  
|DBPROP_ISupportErrorInfo|VARIANT_TRUE|  
|DBPROP_ISequentialStream|VARIANT_TRUE|  
|DBPROP_IMMOBILEROWS|VARIANT_TRUE|  
|DBPROP_LITERALIDENTITY|VARIANT_TRUE|  
|DBPROP_LOCKMODE|DBPROPVAL_LM_NONE|  
|DBPROP_MAXOPENROWS|0|  
|DBPROP_MAXPENDINGROWS|0|  
|DBPROP_MAXROWS|0|  
|DBPROP_NOTIFICATIONPHASES|0|  
|DBPROP_NOTIFYCOLUMNSET DBPROP_NOTIFYROWDELETE DBPROP_NOTIFYROWFIRSTCHANGE DBPROP_NOTIFYROWINSERT DBPROP_NOTIFYROWRESYNCH DBPROP_NOTIFYROWSETRELEASE DBPROP_NOTIFYROWSETFETCH-POSITIONCHANGE DBPROP_NOTIFYROWUNDOCHANGE DBPROP_NOTIFYROWUNDODELETE DBPROP_NOTIFYROWUNDOINSERT DBPROP_NOTIFYROWUPDATE|0|  
|DBPROP_OTHERINSERT DBPROP_OTHERUPDATEDELETE|VARIANT_FALSE|  
|DBPROP_OWNINSERT<br /><br /> DBPROP_OWNUPDATEDELETE|VARIANT_TRUE|  
|DBPROP_QUICKRESTART|VARIANT_TRUE|  
|DBPROP_REENTRANTEVENTS|VARIANT_FALSE|  
|DBPROP_REMOVEDELETED|VARIANT_TRUE|  
|DBPROP_RETURNPENDINGINSERTS|VARIANT_TRUE|  
|DBPROP_ROWRESTRICT|VARIANT_FALSE|  
|DBPROP_ROWTHREADMODEL|DBPROPVAL_RT_FREETHREAD|  
|DBPROP_SERVERCURSOR|VARIANT_FALSE|  
|DBPROP_SERVERDATAONINSERT|VARIANT_FALSE|  
|DBPROP_STRONGIDENTITY|VARIANT_TRUE|  
|DBPROP_TRANSACTEDOBJECT|VARIANT_FALSE|  
|DBPROP_UNIQUEROWS|VARIANT_FALSE|  
|DBPROP_UPDATABILITY|DBPROPVAL_UP_CHANGE &#124; DBPROPVAL_UP_DELETE &#124; DBPROPVAL_UP_INSERT|  
  
## <a name="property-sets"></a>속성 집합  
 下列屬性集支援資料表值參數。  
  
### <a name="dbpropsetsqlservercolumn"></a>DBPROPSET_SQLSERVERCOLUMN  
 這個屬性是由取用者在必要時，利用 ITableDefinitionWithConstraints::CreateTableWithConstraints 透過 DBCOLUMNDESC 結構的每一個資料行建立資料表值參數資料列集物件。  
  
|屬性識別碼|屬性值|  
|-----------------|--------------------|  
|SSPROP_COL_COMPUTED|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 類型：VT_BOOL<br /><br /> 描述：設定為 VARIANT_TRUE 時，表示資料行為計算資料行。 VARIANT_FALSE 則表示它不是計算資料行。|  
  
### <a name="dbpropsetsqlserverparameter"></a>DBPROPSET_SQLSERVERPARAMETER  
 這些屬性由取用者讀取時探索 ISSCommandWithParamters::GetParameterProperties 的呼叫中的資料表值參數類型資訊，設定有關資料表值參數的特定屬性時設定取用者透過 isscommandwithparameters::。  
  
 下表提供這些屬性的詳細描述。  
  
|屬性識別碼|屬性值|  
|-----------------|--------------------|  
|SSPROP_PARAM_TYPE_TYPENAME|R/W：讀取/寫入<br /><br /> 預設值：VT_EMPTY<br /><br /> 類型：VT_BSTR<br /><br /> 描述：取用者會使用這個屬性來取得或設定資料表值參數類型的名稱。<br /><br /> 這個屬性也可以搭配 CLR 使用者定義型別使用。<br /><br /> 您可以選擇性地指定這個屬性來提供資料表值參數的資料表類型名稱 (如果是 ODBC 呼叫語法命令)。 特定參數化的 SQL 查詢需要使用這個屬性。|  
|SSPROP_PARAM_TYPE_SCHEMANAME|R/W：讀取/寫入<br /><br /> 預設值：VT_EMPTY<br /><br /> 類型：VT_BSTR<br /><br /> 描述：取用者會使用這個屬性來取得或設定資料表值參數類型的結構描述名稱。<br /><br /> 這個屬性也可以搭配 CLR 使用者定義型別使用。|  
|SSPROP_PARAM_TYPE_CATALOGNAME|R/W：唯讀<br /><br /> 預設值：VT_EMPTY<br /><br /> 類型：VT_BSTR<br /><br /> 描述：取用者會使用這個屬性來取得資料表值參數類型的目錄名稱。<br /><br /> 這個屬性也可以搭配 CLR 使用者定義型別使用。 設定此屬性是錯誤的；使用者定義資料表類型必須與使用這些類型的資料表值參數位於相同的資料庫中。|  
|SSPROP_PARAM_TABLE_DEFAULT_COLUMNS|R/W：讀取/寫入<br /><br /> 預設值：VT_EMPTY<br /><br /> 類型： VT_UI2 &#124; VT_ARRAY<br /><br /> 描述：取用者會使用這個屬性來指定要將資料列集中的哪組資料行視為預設值。 系統不會針對這些資料行傳送任何值。 從取用者資料列集物件中提取資料時，提供者不需要使用此類資料行的繫結。<br /><br /> 陣列的每個元素都應該是資料列集物件中的資料行序數。 在命令執行階段，無效的序數將會導致錯誤。|  
|SSPROP_PARAM_TABLE_COLUMN_ORDER|R/W：讀取/寫入<br /><br /> 預設值：VT_EMPTY<br /><br /> 類型： VT_UI2 &#124; VT_ARRAY<br /><br /> 描述：取用者會使用此屬性來提供提示給伺服器，指出資料行資料的排序次序。 提供者不會執行任何驗證，並假設取用者符合所提供的規格。 伺服器會使用這個屬性來執行最佳化。<br /><br /> 每個資料行的資料行順序資訊都會以陣列中的一組元素表示。 配對中的第一個元素是資料行的數目。 配對中的第二個元素將為 1 (遞增的順序) 或 2 (遞減的順序)。|  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB 資料表值參數類型支援](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support.md)   
 [使用資料表值參數 & #40; OLE DB & #41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
