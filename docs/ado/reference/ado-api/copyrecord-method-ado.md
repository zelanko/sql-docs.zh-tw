---
title: "CopyRecord 方法 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Record::raw_CopyRecord
- _Record::CopyRecord
helpviewer_keywords:
- CopyRecord method [ADO]
ms.assetid: b9bcf272-3c74-479f-95dd-0229a32e98fc
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5acc04720b17df0c39203417633332a0f01c2890
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="copyrecord-method-ado"></a>CopyRecord 方法 (ADO)
複製所代表的實體[記錄](../../../ado/reference/ado-api/record-object-ado.md)到另一個位置。  
  
## <a name="syntax"></a>語法  
  
```  
  
Record.CopyRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>參數  
 *Source*  
 選擇性。 A**字串**含有 URL 指定實體来複製 （例如，檔案或目錄） 的值。 如果*來源*省略或指定空字串、 檔案或目錄，表示由目前[記錄](../../../ado/reference/ado-api/record-object-ado.md)會被複製。  
  
 *目的地*  
 選擇性。 A**字串**值，其中包含指定位置的 URL 位置*來源*會被複製。  
  
 *UserName*  
 選擇性。 A**字串**值，其中包含的使用者識別碼，如有需要授與存取權*目的地*。  
  
 *密碼*  
 選擇性。 A**字串**包含，如有需要驗證的密碼值*UserName*。  
  
 *選項。*  
 選擇性。 A [CopyRecordOptionsEnum](../../../ado/reference/ado-api/copyrecordoptionsenum.md)具有預設值是值**adCopyUnspecified**。 指定此方法的行為。  
  
 *非同步*  
 選擇性。 A**布林**值，當**True**，指定此作業應該是非同步。  
  
## <a name="return-value"></a>傳回值  
 A**字串**值通常會傳回的值，這個值*目的地*。 不過，傳回的實際值會提供者而異。  
  
## <a name="remarks"></a>備註  
 值*來源*和*目的地*不能相同; 否則就會發生執行階段錯誤。 至少其中一個伺服器、 路徑或資源的名稱必須不同。  
  
 所有子系 （例如，是子目錄）*來源*會以遞迴方式複製，除非**adCopyNonRecursive**指定。 在遞迴作業中，*目的地*不得的子目錄*來源*，否則將無法完成作業。  
  
 如果這個方法會失敗*目的地*識別現有的實體 （例如，檔案或目錄），除非**adCopyOverWrite**指定。  
  
> [!IMPORTANT]
>  使用**adCopyOverWrite**明智選項。 例如，指定這個選項，將檔案複製到目錄時將*刪除*目錄並將它取代檔案。  
  
> [!NOTE]
>  使用 http 配置 Url 將會自動叫用[Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱[絕對和相對 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>適用於  
 [記錄物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)
