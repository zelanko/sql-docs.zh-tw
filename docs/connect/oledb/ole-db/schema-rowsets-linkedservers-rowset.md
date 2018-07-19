---
title: LINKEDSERVERS 資料列集 (OLE DB) |Microsoft 文件
description: LINKEDSERVERS 資料列集 (OLE DB)
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- LINKEDSERVERS rowset
- enumerating data sources [OLE DB]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: ff4c35178b5cc047fb711821b332f43cf0094fc8
ms.sourcegitcommit: 354ed9c8fac7014adb0d752518a91d8c86cdce81
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/14/2018
ms.locfileid: "35611723"
---
# <a name="schema-rowsets---linkedservers-rowset"></a>結構描述資料列集 LINKEDSERVERS 資料列集
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  **LINKEDSERVERS**資料列集會列舉可以參與組織資料來源[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]分散式查詢。  
  
 **LINKEDSERVERS**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|描述|  
|-----------------|--------------------|-----------------|  
|SVR_NAME|DBTYPE_WSTR|連結伺服器的名稱。|  
|SVR_PRODUCT|DBTYPE_WSTR|製造商或是識別由連結伺服器名稱表示之資料存放區類型的其他名稱。|  
|SVR_PROVIDERNAME|DBTYPE_WSTR|用來耗用伺服器中之資料的 OLE DB 提供者易記名稱。|  
|SVR_DATASOURCE|DBTYPE_WSTR|用來從提供者當中取得資料來源的 OLE DB DBPROP_INIT_DATASOURCE 字串。|  
|SVR_PROVIDERSTRING|DBTYPE_WSTR|用來從提供者當中取得資料來源的 OLE DB DBPROP_INIT_PROVIDERSTRING 值。|  
|SVR_LOCATION|DBTYPE_WSTR|用來從提供者當中取得資料來源的 OLE DB DBPROP_INIT_LOCATION 字串。|  
  
 資料列集會根據 SRV_NAME 排序，而且 SRV_NAME 上可支援單一限制。  
  
## <a name="see-also"></a>另請參閱  
 [結構描述資料列集支援&#40;OLE DB&#41;](../../oledb/ole-db/schema-rowset-support-ole-db.md)  
  
  
