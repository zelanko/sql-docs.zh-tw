---
title: MoveRecord 方法（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::MoveRecord
- _Record::raw_MoveRecord
helpviewer_keywords:
- MoveRecord method [ADO]
ms.assetid: 6d2807b0-b861-4583-bcaf-fb0b82e0f2d0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 157e38c2c9c23ff8f7e92af40385b0962c6dcb70
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "67918068"
---
# <a name="moverecord-method-ado"></a>MoveRecord 方法 (ADO)
將[記錄](../../../ado/reference/ado-api/record-object-ado.md)所代表的實體移動到另一個位置。  
  
## <a name="syntax"></a>語法  
  
```  
  
Record.MoveRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>參數  
 *來源*  
 選擇性。 **字串**值，包含可識別要移動之**記錄**的 URL。 如果省略*Source*或指定空字串，則會移動此**記錄**所代表的物件。 例如，如果**記錄**代表檔案，則檔案的內容會移至*目的地*所指定的位置。  
  
 *Destination*  
 選擇性。 包含 URL 的**字串**值，指定將移動*來源*的位置。  
  
 *UserName*  
 選擇性。 包含使用者識別碼的**字串**值，如有需要，會授權存取*目的地*。  
  
 *密碼*  
 選擇性。 包含密碼的**字串**，如有需要則會驗證使用者*名稱*。  
  
 *選項*  
 選擇性。 [MoveRecordOptionsEnum](../../../ado/reference/ado-api/moverecordoptionsenum.md)值，其預設值為**adMoveUnspecified**。 指定此方法的行為。  
  
 *Async*  
 選擇性。 **布林**值，如果**為 True，則**指定此作業應該是非同步。  
  
## <a name="return-value"></a>傳回值  
 **字串**值。 通常會傳回*Destination*的值。 不過，傳回的確切值與提供者相關。  
  
## <a name="remarks"></a>備註  
 *來源*和*目的地*的值不得完全相同;否則，就會發生執行階段錯誤。 至少伺服器、路徑和資源名稱必須不同。  
  
 若為使用網際網路發行提供者移動的檔案，除非由*選項*指定，否則這個方法會更新要移動之檔案中的所有超文字連結。 如果*目的地*識別現有的物件（例如檔案或目錄），則此方法會失敗，除非已指定**adMoveOverWrite** 。  
  
> [!NOTE]
>  請謹慎使用**adMoveOverWrite**選項。 例如，將檔案移至目錄時，指定這個選項將會刪除目錄，並將它取代為檔案。  
  
 在此作業完成之後，**記錄**物件的某些屬性（例如[ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md)屬性）將不會更新。 藉由關閉**記錄**來重新整理**記錄**物件的屬性，然後使用檔案或目錄移動所在位置的 URL 來重新開啟。  
  
 如果此**記錄**是從[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)取得，移動的檔案或目錄的新位置將不會立即反映在**記錄集中**。 關閉並重新開啟**記錄集**，以重新整理它。  
  
> [!NOTE]
>  使用 HTTP 配置的 Url 會自動叫用[Microsoft OLE DB 提供者以進行網際網路發佈](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱[絕對和相對 url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>套用至  
 [Record 物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Move 方法（ADO）](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst、MoveLast、MoveNext 和 MovePrevious 方法（ADO）](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveFirst、MoveLast、MoveNext 和 MovePrevious 方法 (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)
