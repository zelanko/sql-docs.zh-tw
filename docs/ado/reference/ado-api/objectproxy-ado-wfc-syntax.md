---
title: ObjectProxy (ADO-WFC 語法) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 485d011fa6762acd04cad54ff7fffc8d8136e063
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917949"
---
# <a name="objectproxy-ado---wfc-syntax"></a>ObjectProxy (ADO - WFC 語法)
**ObjectProxy**物件代表伺服器，而且由**createObject**方法[DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)物件。 ObjectProxy 類別有一個方法，**呼叫**，其可叫用伺服器上的方法，並傳回該引動過程所產生的物件。  
  
 **封裝 com.ms.wfc.data**  
  
## <a name="methods"></a>方法  
  
### <a name="call-method-adowfc-syntax"></a>呼叫方法 （ADO/WFC 語法）  
 叫用 ObjectProxy 所代表的伺服器上的方法。 （選擇性） 方法的引數可能會傳遞為物件的陣列。  
  
#### <a name="syntax"></a>語法  
  
```  
public Object ObjectProxy.( String method )  
public Object ObjectProxy.( String method, Object[] args)  
```  
  
#### <a name="returns"></a>傳回值  
 Object  
 叫用方法所產生的物件。  
  
#### <a name="parameters"></a>參數  
 *ObjectProxy*  
 **ObjectProxy**代表伺服器的物件。  
  
 *方法*  
 字串，包含要叫用伺服器上的方法名稱。  
  
 *引數*  
 選擇性。 是在伺服器上方法的引數的物件的陣列。 Java 資料類型會自動轉換成適用於在伺服器上使用的資料類型。
