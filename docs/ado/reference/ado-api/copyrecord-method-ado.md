---
title: CopyRecord 方法（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_CopyRecord
- _Record::CopyRecord
helpviewer_keywords:
- CopyRecord method [ADO]
ms.assetid: b9bcf272-3c74-479f-95dd-0229a32e98fc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aaabb32234cefe2e3c3727ce5a18dd2d98549a77
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67933410"
---
# <a name="copyrecord-method-ado"></a>CopyRecord 方法 (ADO)
將[記錄](../../../ado/reference/ado-api/record-object-ado.md)所代表的實體複製到另一個位置。  
  
## <a name="syntax"></a>語法  
  
```  
  
Record.CopyRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>參數  
 *來源*  
 選擇性。 **字串**值，其中包含指定要複製之實體的 URL （例如，檔案或目錄）。 如果省略*Source*或指定空字串，則會複製目前[記錄](../../../ado/reference/ado-api/record-object-ado.md)所代表的檔案或目錄。  
  
 *Destination*  
 選擇性。 **字串**值，其中包含指定要複製*來源*之位置的 URL。  
  
 *UserName*  
 選擇性。 包含使用者識別碼的**字串**值，如有需要，會授權存取*目的地*。  
  
 *密碼*  
 選擇性。 包含密碼的**字串**值（如有需要）會驗證使用者*名稱*。  
  
 *選項*  
 選擇性。 [CopyRecordOptionsEnum](../../../ado/reference/ado-api/copyrecordoptionsenum.md)值，其預設值為**adCopyUnspecified**。 指定此方法的行為。  
  
 *Async*  
 選擇性。 **布林**值，如果**為 True，則**指定此作業應該是非同步。  
  
## <a name="return-value"></a>傳回值  
 通常會傳回*目的地*值的**字串**值。 不過，傳回的確切值與提供者相關。  
  
## <a name="remarks"></a>備註  
 *來源*和*目的地*的值不得完全相同;否則，就會發生執行階段錯誤。 至少其中一個伺服器、路徑或資源名稱必須不同。  
  
 除非指定**adCopyNonRecursive** ，否則會以遞迴方式複製*來源*的所有子系（例如子目錄）。 在遞迴作業中， *Destination*不得為*Source*的子目錄;否則，作業將不會完成。  
  
 如果*目的地*識別現有的實體（例如檔案或目錄），則此方法會失敗，除非已指定**adCopyOverWrite** 。  
  
> [!IMPORTANT]
>  請謹慎使用**adCopyOverWrite**選項。 例如，將檔案複製到目錄時，指定這個選項將會*刪除*目錄，並將它取代為檔案。  
  
> [!NOTE]
>  使用 HTTP 配置的 Url 會自動叫用[Microsoft OLE DB 提供者以進行網際網路發佈](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱[絕對和相對 url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>套用至  
 [Record 物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)
