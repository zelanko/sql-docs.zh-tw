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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: deca1648d6ef4f9ba3a1dfd020dc5193c8cc0d25
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932427"
---
# <a name="idsoshapeextensions-interface"></a>IDSOShapeExtensions 介面
SHAPE 提供者取得基礎 OLE DB 資料來源物件。  
  
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
  
|||  
|-|-|  
|[GetDataProviderDSO 方法](../../../ado/reference/ado-api/getdataproviderdso-method.md)|從 Shape 提供者擷取基礎 OLE DB 資料來源物件。|  
  
## <a name="requirements"></a>需求  
 **版本：** ADO 2.0 和更新版本  
  
 **程式庫：** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4
