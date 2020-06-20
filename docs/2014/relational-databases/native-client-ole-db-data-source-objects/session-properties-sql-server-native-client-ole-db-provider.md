---
title: 會話屬性 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 99f2bc6def0f470f653446c87216c3e854b2f819
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85056337"
---
# <a name="session-properties"></a>工作階段屬性
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者會解讀 OLE DB 會話屬性，如下所示。  
  
|屬性識別碼|描述|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]除了混亂層級 DBPROPVAL_TI_CHAOS 以外，Native Client OLE DB 提供者支援所有的自動認可交易隔離等級。|  
  
 在提供者特定的屬性集 DBPROPSET_SQLSERVERSESSION 中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會定義下列額外的會話屬性。  
  
|屬性識別碼|描述|  
|-----------------|-----------------|  
|SSPROP_QUOTEDCATALOGNAMES|輸入：VT_BOOL<br /><br /> R/W︰讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述：CATALOG 限制中允許引號識別碼。<br /><br /> VARIANT_TRUE：辨識出引號識別碼有提供分散式查詢支援之結構描述資料列集的目錄限制。<br /><br /> VARIANT_FALSE：未辨識出引號識別碼有提供分散式查詢支援之結構描述資料列集的目錄限制。<br /><br /> 如需提供分散式查詢支援之結構描述資料列集的詳細資訊，請參閱[結構描述資料列集中的分散式查詢支援](../native-client/ole-db/schema-rowsets-distributed-query-support.md)。|  
|SSPROP_ALLOWNATIVEVARIANT|輸入：VT_BOOL<br /><br /> R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述：決定所提取的資料是否為 DBTYPE_VARIANT 或 DBTYPE_SQLVARIANT。<br /><br /> VARIANT_TRUE：資料行類型是以 DBTYPE_SQLVARIANT 傳回，在此種情況下，緩衝區會保存 SSVARIANT 結構。<br /><br /> VARIANT_FALSE：資料行類型是以 DBTYPE_VARIANT 傳回，而且緩衝區將具有 VARIANT 結構。|  
|SSPROP_ASYNCH_BULKCOPY|若要使用非同步模式，請在呼叫 BCPExec 方法之前將提供者特有的工作階段屬性 SSPROP_ASYNCH_BULKCOPY 設定為 VARIANT_TRUE。 DBPROPSET_SQLSERVERSESSION 屬性集中有提供這個屬性。|  
  
## <a name="see-also"></a>另請參閱  
 [資料來源物件 &#40;OLE DB&#41;](data-source-objects-ole-db.md)  
  
  
