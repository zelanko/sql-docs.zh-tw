---
description: IDSOShapeExtensions 介面
title: IDSOShapeExtensions 介面 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- IDSOShapeExtensions interface [ADO]
ms.assetid: ad4ba313-1161-4bc7-b8f6-4083305bc81e
author: rothja
ms.author: jroth
ms.openlocfilehash: 7adf307020dd820b828a48a255e6c552c51f6efd
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990819"
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
|[GetDataProviderDSO 方法](./getdataproviderdso-method.md)|從圖形提供者抓取基礎 OLE DB 資料來源物件。|  
  
## <a name="requirements"></a>規格需求  
 **版本：** ADO 2.0 和更新版本  
  
 連結**庫：** msado15.dll  
  
 **UUID：** 00000283-0000-0010-8000-00AA006D2EA4