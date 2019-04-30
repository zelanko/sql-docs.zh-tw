---
title: Charset 屬性 (ADO) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 20fff124f33bfeccaec665c74687753e2c0af20b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63239746"
---
# <a name="charset-property-ado"></a>Charset 屬性 (ADO)
指出字元集所在的文字內容[Stream](../../../ado/reference/ado-api/stream-object-ado.md)應轉譯為儲存體中的內部緩衝區**Stream**物件。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**字串**指定的字元的值設定到其中的內容**Stream**會轉譯。 預設值是**Unicode**。 允許的值是透過介面傳遞做為網際網路的字元組名稱 （例如，"iso-8859-1"、"Windows-1252"等等） 的一般字串。 如需已知由系統的字元組名稱的清單，請參閱 HKEY_CLASSES_ROOT\MIME\Database\Charset Windows 登錄中的子機碼。  
  
## <a name="remarks"></a>備註  
 以文字**Stream**物件，文字資料會儲存在所指定的字元集**字元集**屬性。 預設值為 Unicode。 **Charset**屬性用來轉換資料持續進入**Stream**或即將共**Stream**。 例如，如果**Stream**包含 ISO-8859-1 資料和資料會複製到的 BSTR **Stream**物件會將資料轉換成 Unicode。 反之亦然。  
  
 為開啟**Stream**，目前[位置](../../../ado/reference/ado-api/position-property-ado.md)的開頭必須是**Stream** (0)，若要能夠設定**Charset**。  
  
 **Charset**僅適用於文字**Stream**物件 ([類型](../../../ado/reference/ado-api/type-property-ado-stream.md)是**adTypeText**)。 如果此屬性則會忽略**型別**是**adTypeBinary**。  
  
 如需程式碼範例，請參閱[步驟 4:填入詳細資料 文字方塊](../../../ado/guide/data/step-4-populate-the-details-text-box.md)。  
  
## <a name="applies-to"></a>適用於  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
