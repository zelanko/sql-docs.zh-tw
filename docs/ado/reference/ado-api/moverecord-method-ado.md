---
description: MoveRecord 方法 (ADO)
title: " (ADO) 的 MoveRecord 方法 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3425326f9693d7c411f97f04ab5f87bba46578b4
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990509"
---
# <a name="moverecord-method-ado"></a>MoveRecord 方法 (ADO)
將 [記錄](./record-object-ado.md) 所代表的實體移至另一個位置。  
  
## <a name="syntax"></a>語法  
  
```  
  
Record.MoveRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>參數  
 *Source*  
 選擇性。 **字串**值，包含識別要移動之**記錄**的 URL。 如果省略 *Source* 或指定空字串，則會移動此 **記錄** 所表示的物件。 例如，如果 **記錄** 代表檔案，則檔案的內容會移至 *目的地*所指定的位置。  
  
 *目的地*  
 選擇性。 **字串**值，包含指定將移動*來源*之位置的 URL。  
  
 *UserName*  
 選擇性。 包含使用者識別碼的 **字串** 值（如有需要）會授權存取 *目的地*。  
  
 *密碼*  
 選擇性。 包含密碼的 **字串** （如有需要，會驗證使用者 *名稱*）。  
  
 *選項*  
 選擇性。 [MoveRecordOptionsEnum](./moverecordoptionsenum.md)值，其預設值為**adMoveUnspecified**。 指定此方法的行為。  
  
 *非同步*  
 選擇性。 **布林**值，若**為 True，則**指定這是非同步作業。  
  
## <a name="return-value"></a>傳回值  
 **字串**值。 通常會傳回 *目的地* 的值。 不過，傳回的確切值與提供者相依。  
  
## <a name="remarks"></a>備註  
 *來源*和*目的地*的值不得相同;否則，就會發生執行階段錯誤。 至少伺服器、路徑和資源名稱必須不同。  
  
 針對使用網際網路發佈提供者移動的檔案，這個方法會更新要移動之檔案中的所有超文字連結，除非 *選項*另有指定。 如果 *目的地* 識別現有的物件 (例如，檔案或目錄) ，除非指定了 **adMoveOverWrite** ，否則這個方法會失敗。  
  
> [!NOTE]
>  謹慎使用 **adMoveOverWrite** 選項。 例如，將檔案移至目錄時，指定這個選項會刪除目錄，並將它取代為檔案。  
  
 在此作業完成之後，將不會更新 **記錄** 物件的某些屬性，例如 [ParentURL](./parenturl-property-ado.md) 屬性。 藉由關閉**記錄**來重新整理**記錄**物件的屬性，然後以移動檔案或目錄的位置 URL 重新開啟它。  
  
 如果從[記錄集](./recordset-object-ado.md)取得此**記錄**，移動的檔案或目錄的新位置將不會立即反映在**記錄集中**。 關閉並重新開啟記錄集，以重新整理 **記錄集** 。  
  
> [!NOTE]
>  使用 HTTP 配置的 Url 會自動叫用 [Microsoft OLE DB 提供者進行網際網路發佈](../../guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱 [絕對和相對 url](../../guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>套用至  
 [Record 物件 (ADO)](./record-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO) 的 Move 方法 ](./move-method-ado.md)   
 [MoveFirst、MoveLast、MoveNext 和 MovePrevious 方法 (ADO) ](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveFirst、MoveLast、MoveNext 和 MovePrevious 方法 (RDS)](../rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)