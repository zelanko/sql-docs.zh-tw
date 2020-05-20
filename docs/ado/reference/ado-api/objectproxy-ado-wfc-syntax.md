---
title: ObjectProxy （ADO-WFC 語法） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ObjectProxy collection [ADO]
ms.assetid: f68f58bc-ad28-46cc-9fb3-099e1a678397
author: rothja
ms.author: jroth
ms.openlocfilehash: ff9cd79b4ac787987ef44ea3f73cbd9fb102ae43
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762317"
---
# <a name="objectproxy-ado---wfc-syntax"></a>ObjectProxy (ADO - WFC 語法)
**ObjectProxy**物件代表伺服器，而且是由量[空間](../../../ado/reference/rds-api/dataspace-object-rds.md)物件的**createObject**方法所傳回。 ObjectProxy 類別有一個方法 call，它可以**叫**用伺服器上的方法，並傳回該調用所產生的物件。  
  
 **封裝 .com. wfc. 資料**  
  
## <a name="methods"></a>方法  
  
### <a name="call-method-adowfc-syntax"></a>Call 方法（ADO/WFC 語法）  
 在 ObjectProxy 所代表的伺服器上叫用方法。 或者，可以將方法引數當做物件的陣列傳遞。  
  
#### <a name="syntax"></a>語法  
  
```  
public Object ObjectProxy.( String method )  
public Object ObjectProxy.( String method, Object[] args)  
```  
  
#### <a name="returns"></a>傳回  
 Object  
 叫用方法所產生的物件。  
  
#### <a name="parameters"></a>參數  
 *ObjectProxy*  
 代表伺服器的**ObjectProxy**物件。  
  
 *方法*  
 字串，包含要在伺服器上叫用之方法的名稱。  
  
 *引數*  
 選擇性。 物件的陣列，這是伺服器上方法的引數。 JAVA 資料類型會自動轉換成適合在伺服器上使用的資料類型。
