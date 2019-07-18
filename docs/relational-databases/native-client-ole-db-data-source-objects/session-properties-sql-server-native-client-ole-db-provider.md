---
title: 工作階段屬性-SQL Server Native Client OLE DB 提供者 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- sessions [OLE DB]
- SQL Server Native Client OLE DB provider, sessions
ms.assetid: 2498fbad-b3db-4bea-8fc6-fef5317d3eba
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d17b673a12a915318e523000081fcd6114e8185c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68128545"
---
# <a name="session-properties---sql-server-native-client-ole-db-provider"></a>工作階段屬性 - SQL Server Native Client OLE DB 提供者
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者解譯的 OLE DB 工作階段屬性，如下所示。  
  
|屬性識別碼|描述|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者支援所有自動認可交易隔離等級，但是混亂等級 dbpropval_ti_chaos 除外。|  
  
 在提供者專用的屬性集 DBPROPSET_SQLSERVERSESSION 中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會定義下列額外的工作階段屬性。  
  
|屬性識別碼|描述|  
|-----------------|-----------------|  
|SSPROP_QUOTEDCATALOGNAMES|類型：VT_BOOL<br /><br /> R/W:讀取/寫入<br /><br /> 預設：VARIANT_FALSE<br /><br /> 描述：引號 CATALOG 限制中允許的識別項。<br /><br /> VARIANT_TRUE:辨識出引號的識別碼有提供分散式的查詢支援之結構描述資料列集的目錄限制。<br /><br /> VARIANT_FALSE:提供分散式的查詢支援之結構描述資料列集的目錄限制不會辨識出引號的識別碼。<br /><br /> 如需提供分散式查詢支援之結構描述資料列集的詳細資訊，請參閱[結構描述資料列集中的分散式查詢支援](../../relational-databases/native-client/ole-db/schema-rowsets-distributed-query-support.md)。|  
|SSPROP_ALLOWNATIVEVARIANT|類型：VT_BOOL<br /><br /> R/W:讀取/寫入<br /><br /> 預設：VARIANT_FALSE<br /><br /> 描述：判斷是否為 DBTYPE_VARIANT 或 DBTYPE_SQLVARIANT 提取的資料。<br /><br /> VARIANT_TRUE:資料行類型會傳回為 DBTYPE_SQLVARIANT，在此案例的緩衝區會保存 SSVARIANT 結構。<br /><br /> VARIANT_FALSE:資料行類型以 DBTYPE_VARIANT 傳回，緩衝區將具有 VARIANT 結構。|  
|SSPROP_ASYNCH_BULKCOPY|若要使用非同步模式，請在呼叫 BCPExec 方法之前將提供者特有的工作階段屬性 SSPROP_ASYNCH_BULKCOPY 設定為 VARIANT_TRUE。 DBPROPSET_SQLSERVERSESSION 屬性集中有提供這個屬性。|  
  
## <a name="see-also"></a>另請參閱  
 [資料來源物件&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
