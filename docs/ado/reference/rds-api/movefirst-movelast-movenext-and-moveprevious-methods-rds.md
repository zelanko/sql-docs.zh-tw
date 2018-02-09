---
title: "MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法 (RDS) |Microsoft 文件"
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
helpviewer_keywords:
- MoveLast method [RDS]
- MovePrevious method [RDS]
- MoveFirst method [RDS]
- MoveNext method [RDS]
ms.assetid: 45c80bb5-136f-4204-9df2-78740fa55574
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3e1896722849690331e88a4b426a6491bb19ee8c
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-rds"></a>MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法 (RDS)
移至 [first、 last、 在指定的下一步]，或上一個記錄[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
DataControl.Recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
#### <a name="parameters"></a>參數  
 *DataControl*  
 物件變數，表示[.RDSDataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件。  
  
## <a name="remarks"></a>備註  
 您可以使用**移動**方法**.RDSDataControl**來瀏覽資料記錄，在網頁上的資料繫結控制項中的物件。 例如，假設您顯示**資料錄集**繫結至方格中**.RDSDataControl**物件。 接著，您可以加入 First、 Last、 下一步及上一步 按鈕讓使用者可以按一下以移至第一個、 最後一個、 下一步，或在顯示上一筆記錄**資料錄集**。 您可以呼叫**MoveFirst**， **MoveLast**， **MoveNext**，和**MovePrevious**方法**.RDSDataControl**分別物件存放至 First、 Last、 下一步及上一步按鈕的 onClick 程序。 [通訊錄範例](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md)示範如何執行這項操作。  
  
## <a name="applies-to"></a>適用於  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [Move 方法 (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法 (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveRecord 方法 (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)


