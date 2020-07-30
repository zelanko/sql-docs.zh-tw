---
title: IDSOShapeExtensions 介面 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- IDSOShapeExtensions interface [ADO]
ms.assetid: ad4ba313-1161-4bc7-b8f6-4083305bc81e
author: rothja
ms.author: jroth
ms.openlocfilehash: 02eedbeaf8c9d85f3a896b8991661461825b2b19
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242668"
---
# <a name="idsoshapeextensions-interface"></a>IDSOShapeExtensions 介面
取得圖形提供者的基礎 OLE DB 資料來源物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
interface IDSOShapeExtensions: public IUnknown {  
public:  
      HRESULT  GetDataProviderDSO(  
            IUnknown **ppDataProviderDSOIUnknown  
      );  
};  
```  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|-|-|  
|[GetDataProviderDSO 方法](../../../ado/reference/ado-api/getdataproviderdso-method.md)|從圖形提供者抓取基礎 OLE DB 資料來源物件。|  
  
## <a name="requirements"></a>需求  
 **版本：** ADO 2.0 和更新版本  
  
 連結**庫：** msado15.dll  
  
 **UUID：** 00000283-0000-0010-8000-00AA006D2EA4
