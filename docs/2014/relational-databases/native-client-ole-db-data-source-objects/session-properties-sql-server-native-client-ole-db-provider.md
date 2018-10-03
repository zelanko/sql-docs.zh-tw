---
title: 工作階段屬性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- sessions [OLE DB]
- SQL Server Native Client OLE DB provider, sessions
ms.assetid: 2498fbad-b3db-4bea-8fc6-fef5317d3eba
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 19ce2c6ca7b36a5d2147e7efda657fb2433aef25
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48158698"
---
# <a name="session-properties"></a>工作階段屬性
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者解譯的 OLE DB 工作階段屬性，如下所示。  
  
|屬性識別碼|描述|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者支援所有自動認可交易隔離等級，但是混亂等級 dbpropval_ti_chaos 除外。|  
  
 在提供者專用的屬性集 DBPROPSET_SQLSERVERSESSION 中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會定義下列額外的工作階段屬性。  
  
|屬性識別碼|描述|  
|-----------------|-----------------|  
|SSPROP_QUOTEDCATALOGNAMES|類型：VT_BOOL<br /><br /> R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述：CATALOG 限制中允許引號識別碼。<br /><br /> VARIANT_TRUE：辨識出引號識別碼有提供分散式查詢支援之結構描述資料列集的目錄限制。<br /><br /> VARIANT_FALSE：未辨識出引號識別碼有提供分散式查詢支援之結構描述資料列集的目錄限制。<br /><br /> 如需提供分散式查詢支援之結構描述資料列集的詳細資訊，請參閱[結構描述資料列集中的分散式查詢支援](../native-client/ole-db/schema-rowsets-distributed-query-support.md)。|  
|SSPROP_ALLOWNATIVEVARIANT|類型：VT_BOOL<br /><br /> R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述：決定所提取的資料是否為 DBTYPE_VARIANT 或 DBTYPE_SQLVARIANT。<br /><br /> VARIANT_TRUE：資料行類型是以 DBTYPE_SQLVARIANT 傳回，在此種情況下，緩衝區會保存 SSVARIANT 結構。<br /><br /> VARIANT_FALSE：資料行類型是以 DBTYPE_VARIANT 傳回，而且緩衝區將具有 VARIANT 結構。|  
|SSPROP_ASYNCH_BULKCOPY|若要使用非同步模式，請在呼叫 BCPExec 方法之前將提供者特有的工作階段屬性 SSPROP_ASYNCH_BULKCOPY 設定為 VARIANT_TRUE。 DBPROPSET_SQLSERVERSESSION 屬性集中有提供這個屬性。|  
  
## <a name="see-also"></a>另請參閱  
 [資料來源物件&#40;OLE DB&#41;](data-source-objects-ole-db.md)  
  
  
