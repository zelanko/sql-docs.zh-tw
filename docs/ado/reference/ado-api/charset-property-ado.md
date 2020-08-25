---
description: Charset 屬性 (ADO)
title: " (ADO) 的字元集屬性 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Charset
helpviewer_keywords:
- Charset property [ADO]
ms.assetid: e42507cb-9b46-4ce4-8191-2948eaf14ca2
author: rothja
ms.author: jroth
ms.openlocfilehash: 898f0bdb7571d31d1d7e943bae0937ce198433ce
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776277"
---
# <a name="charset-property-ado"></a>Charset 屬性 (ADO)
表示要在**資料流程**物件的內部緩衝區中，轉譯文字[資料流程](./stream-object-ado.md)內容以進行儲存的字元集。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回 **字串** 值，這個值會指定要轉譯 **資料流程** 內容的字元集。 預設值為 **Unicode**。 允許的值是以網際網路字元集名稱形式傳遞給介面的一般字串 (例如，"iso-8859-1"、"Windows-1252" 等) 。 如需系統已知的字元集名稱清單，請參閱 Windows 登錄中 HKEY_CLASSES_ROOT \MIME\Database\Charset 的子機碼。  
  
## <a name="remarks"></a>備註  
 在文字 **資料流程** 物件中，文字資料會儲存在 **字元集** 屬性所指定的字元集中。 預設值為 Unicode。 [ **字元集** ] 屬性是用來將資料轉換成 **資料流程** 或 **流出資料流程**。 例如，如果 **資料流程** 包含 ISO-8859-1 資料，而該資料會複製到 BSTR， **資料流程** 物件就會將資料轉換成 Unicode。 反之亦然。  
  
 針對開啟的 **資料流程**，目前的 [位置](./position-property-ado.md) 必須位於 **資料流程** 的開頭 (0) 才能設定 **字元集**。  
  
 **字元集** 僅適用于文字 **資料流程** 物件， ([類型](./type-property-ado-stream.md) 為 **adTypeText**) 。 如果 **類型** 為 **adTypeBinary**，則會忽略這個屬性。  
  
 如需程式碼範例，請參閱 [步驟4：填入詳細資料文字方塊](../../guide/data/step-4-populate-the-details-text-box.md)。  
  
## <a name="applies-to"></a>套用至  
 [Stream 物件 (ADO)](./stream-object-ado.md)