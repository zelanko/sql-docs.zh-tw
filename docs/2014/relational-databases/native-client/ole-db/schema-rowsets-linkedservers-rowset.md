---
title: LINKEDSERVERS 資料列集 (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- LINKEDSERVERS rowset
- enumerating data sources [OLE DB]
ms.assetid: 2633fd8a-65e7-498d-9aed-8e4b1cca2381
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a136e3b2064e42e6bae7cfb39f059dbaa41a8410
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48159088"
---
# <a name="linkedservers-rowset-ole-db"></a>LINKEDSERVERS 資料列集 (OLE DB)
  **LINKEDSERVERS** 資料列集會列舉可以參與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分散式查詢的組織資料來源。  
  
 **LINKEDSERVERS** 資料列集包含下列資料行。  
  
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
 [結構描述資料列集支援 &#40;OLE DB&#41;](schema-rowset-support-ole-db.md)  
  
  
