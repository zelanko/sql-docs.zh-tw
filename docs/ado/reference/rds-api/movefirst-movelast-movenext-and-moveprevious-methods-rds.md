---
description: MoveFirst、MoveLast、MoveNext 和 MovePrevious 方法 (RDS)
title: " (RDS) 的 MoveFirst、MoveLast、MoveNext 和 MovePrevious 方法 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: e0e2b53967017ca093b04b5449ebd7a47a983f29
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724469"
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-rds"></a>MoveFirst、MoveLast、MoveNext 和 MovePrevious 方法 (RDS)
移至指定之 [記錄集](../ado-api/recordset-object-ado.md) 物件中的第一個、最後一個、下一個或上一個記錄。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](/dotnet/framework/wcf/)。  
  
## <a name="syntax"></a>語法  
  
```  
  
DataControl.Recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
#### <a name="parameters"></a>參數  
 *DataControl*  
 代表 RDS 的物件變數 [。DataControl](./datacontrol-object-rds.md) 物件。  
  
## <a name="remarks"></a>備註  
 您可以使用 **Move** 方法搭配 **RDS。DataControl** 物件，以流覽網頁上資料繫結控制項中的資料記錄。 例如，假設您藉由系結至 RDS，在方格中顯示 **記錄集** **。DataControl** 物件。 然後，您可以包含 [第一個]、[最後]、[下一步] 和 [上一個] 按鈕，讓使用者按一下以移至所顯示 **記錄集中**的第一個、最後一個、最後一個或上一個 若要這麼做，請呼叫 RDS 的 **MoveFirst**、 **MoveLast**、 **MoveNext**和 **MovePrevious** 方法 **。** 分別是第一個、最後一個、下一個和先前按鈕的 onClick 程式中的 DataControl 物件。 [通訊錄範例](../../guide/remote-data-service/address-book-navigation-buttons.md)會示範如何進行此作業。  
  
## <a name="applies-to"></a>套用至  
 [DataControl 物件 (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO) 的 Move 方法 ](../ado-api/move-method-ado.md)   
 [MoveFirst、MoveLast、MoveNext 和 MovePrevious 方法 (ADO) ](../ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveRecord 方法 (ADO)](../ado-api/moverecord-method-ado.md)