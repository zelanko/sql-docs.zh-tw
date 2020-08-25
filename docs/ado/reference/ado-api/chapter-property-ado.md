---
description: Chapter 屬性 (ADO)
title: " (ADO) 的章節屬性 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordsetConstruction::Chapter
- ADORecordsetConstruction::put_Chapter
- ADORecordsetConstruction::get_Chapter
helpviewer_keywords:
- Chapter property [ADO]
ms.assetid: 8aa90cb0-f588-4141-9dc9-3b22918394ee
author: rothja
ms.author: jroth
ms.openlocfilehash: 04469dc7cc888a167135ad18a77469200614e925
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776297"
---
# <a name="chapter-property-ado"></a>Chapter 屬性 (ADO)
從[ADORecordsetConstruction 介面](./adorecordsetconstruction-interface.md)物件取得或設定 OLE DB**章節**物件。 當您使用 **put_Chapter** 設定 **章節** 物件時，資料列的子集會轉換成 ADO [記錄集物件](./recordset-object-ado.md) 物件。 這會設定資料列 **集**物件的目前章節。 這是可讀寫的屬性。  
  
## <a name="syntax"></a>語法  
  
```  
HRESULT get_Chapter([out, retval] long* plChapter);  
HRESULT put_Chapter([in] long lChapter);  
```  
  
## <a name="parameters"></a>參數  
 *plChapter*  
 章節的控制碼指標。  
  
 *LChapter*  
 章節的控制碼。  
  
## <a name="return-values"></a>傳回值  
 這個屬性方法會傳回標準的 HRESULT 值，包括 S_OK 和 E_FAIL。  
  
## <a name="applies-to"></a>套用至  
 [ADORecordsetConstruction 介面](./adorecordsetconstruction-interface.md)