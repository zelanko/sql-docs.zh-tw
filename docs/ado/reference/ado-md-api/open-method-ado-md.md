---
description: Open 方法 (ADO MD)
title: 開啟方法 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Open
- Cellset::Open
helpviewer_keywords:
- Open method [ADO MD]
ms.assetid: a87d8080-a238-45e5-bc80-9a8625b3810f
author: rothja
ms.author: jroth
ms.openlocfilehash: 56d6a216b7d21723d84d374b09a9c0b8c6c4806b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440820"
---
# <a name="open-method-ado-md"></a>Open 方法 (ADO MD)
抓取多維度查詢的結果，並將結果傳回至 [儲存格集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
Cellset.Open Source, ActiveConnection  
```  
  
#### <a name="parameters"></a>參數  
 *Source*  
 選擇性。 判斷值為有效多維度查詢的 **Variant** ，例如多維度運算式 (MDX) 查詢。 *來源*引數對應至[來源](../../../ado/reference/ado-md-api/source-property-ado-md.md)屬性。 如需 MDX 的詳細資訊，請參閱 Microsoft Data Access Components SDK 中的 [線上分析處理 (OLAP) ](https://msdn.microsoft.com/8a7673c6-3ca1-4411-9f1e-adf1e47df4f3) 檔的 OLE DB。  
  
 *ActiveConnection*  
 選擇性。 此 **變數** 會評估為字串，以指定有效的 ADO [連接](../../../ado/reference/ado-api/connection-object-ado.md) 物件變數名稱或連接的定義。 *ActiveConnection*引數會指定要在其中開啟[儲存格](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)物件的連接。 如果您傳遞此引數的連接定義，ADO 會使用指定的參數開啟新的連接。 *ActiveConnection*引數會對應至[ActiveConnection](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md)屬性。  
  
## <a name="remarks"></a>備註  
 如果省略了其中一個參數，且未在嘗試開啟該**儲存格**之前設定其對應的屬性值，則**Open**方法會產生錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Cellset 物件 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB) 的集格範例 ](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [ActiveConnection 屬性 (ADO MD) ](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md)   
 [關閉方法 (ADO MD) ](../../../ado/reference/ado-md-api/close-method-ado-md.md)   
 [ (ADO) 的 Connection 物件 ](../../../ado/reference/ado-api/connection-object-ado.md)   
 [來源屬性 (ADO MD) ](../../../ado/reference/ado-md-api/source-property-ado-md.md)   
 [State 屬性 (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)
