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
author: rothja
ms.author: jroth
ms.openlocfilehash: 67814e1236bc10e9b008d1684586796dd62950b4
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759554"
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
