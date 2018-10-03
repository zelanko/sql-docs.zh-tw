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
manager: craigg
ms.openlocfilehash: af28755fee20c478237edec22936fc694995d554
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47678506"
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
