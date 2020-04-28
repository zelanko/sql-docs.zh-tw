---
title: StringFormatEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StringFormatEnum
helpviewer_keywords:
- StringFormatEnum enumeration [ADO]
ms.assetid: 28f7d1ec-092b-4323-a39d-d3f882c6c81a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 85bef64902f014e7b5269d6df328128bc8fe8d6e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67937886"
---
# <a name="stringformatenum"></a>StringFormatEnum
指定以字串形式抓取[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)時的格式。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adClipString**|2|藉由依*RowDelimiter*、依*ColumnDelimiter*的資料行，以及*NullExpr*的 null 值分隔資料列。 這三個[GetString](../../../ado/reference/ado-api/getstring-method-ado.md)方法的參數僅適用于**adClipString**的*StringFormat* 。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 Package： **.com. wfc. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums.StringFormat.CLIPSTRING|  
  
## <a name="applies-to"></a>套用至  
 [GetString 方法 (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)
