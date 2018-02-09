---
title: "字元集屬性 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Stream::Charset
helpviewer_keywords:
- Charset property [ADO]
ms.assetid: e42507cb-9b46-4ce4-8191-2948eaf14ca2
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 43d23eda107933ab659324de412db0e101f8da00
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="charset-property-ado"></a>字元集屬性 (ADO)
指出字元集所在的文字內容[資料流](../../../ado/reference/ado-api/stream-object-ado.md)應轉譯的內部緩衝區中的儲存體**資料流**物件。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**字串**指定字元的值設定到其中的內容**資料流**將轉譯。 預設值是**Unicode**。 允許的值是透過介面傳遞做為網際網路的字元組名稱 （例如，"iso-8859-1"、"windows-1252"，等等） 的一般字串。 如需的系統使用已知的字元組名稱清單，請參閱 HKEY_CLASSES_ROOT\MIME\Database\Charset Windows 登錄中的子機碼。  
  
## <a name="remarks"></a>備註  
 在文字中**資料流**物件時，文字資料會儲存在所指定字元集**Charset**屬性。 預設值為 Unicode。 **Charset**屬性用來轉換資料持續進入**資料流**或未來超出**資料流**。 例如，如果**資料流**包含 ISO 8859-1 的資料和資料會複製到 BSTR、**資料流**物件會將資料轉換成 Unicode。 反之亦然。  
  
 為開啟**資料流**，目前[位置](../../../ado/reference/ado-api/position-property-ado.md)的開頭必須是**資料流**(0) 可以設定**Charset**。  
  
 **Charset**僅適用於文字**資料流**物件 ([類型](../../../ado/reference/ado-api/type-property-ado-stream.md)是**adTypeText**)。 如果這個屬性就會忽略**類型**是**adTypeBinary**。  
  
 如需程式碼範例，請參閱[步驟 4： 填入 [詳細資料] 文字方塊中](../../../ado/guide/data/step-4-populate-the-details-text-box.md)。  
  
## <a name="applies-to"></a>適用於  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
