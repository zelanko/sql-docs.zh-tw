---
title: MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法 (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- MoveLast method [RDS]
- MovePrevious method [RDS]
- MoveFirst method [RDS]
- MoveNext method [RDS]
ms.assetid: 45c80bb5-136f-4204-9df2-78740fa55574
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3afc55ca26a8462eb5662287288ee885f9104a8c
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2018
ms.locfileid: "51606676"
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-rds"></a>MoveFirst、MoveLast、MoveNext 和 MovePrevious 方法 (RDS)
移至 [first、 last、 下一步]，或上一個記錄中指定[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
DataControl.Recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
#### <a name="parameters"></a>參數  
 *DataControl*  
 物件變數，表示[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件。  
  
## <a name="remarks"></a>備註  
 您可以使用**移動**方法**rds。DataControl**來瀏覽網頁上的資料繫結控制項中的資料記錄的物件。 比方說，假設您顯示**Recordset**繫結至方格中**rds。DataControl**物件。 您即可接著把第一個、 最後一個下, 一步 和上一步 按鈕，使用者可以按一下以移至第一個、 last、 下一步，或在顯示上一筆記錄**資料錄集**。 您可以呼叫**MoveFirst**， **MoveLast**， **MoveNext**，以及**MovePrevious**方法**rds。DataControl**分別物件中第一個、 Last、 下一步 和上一步 按鈕的 onClick 程序。 [通訊錄範例](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md)示範如何執行這項操作。  
  
## <a name="applies-to"></a>適用於  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [Move 方法 (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法 (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveRecord 方法 (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)


