---
description: NextRecordset 方法 (ADO)
title: " (ADO) 的 NextRecordset 方法 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- NextRecordset
- Recordset15::NextRecordset
- Recordset15::raw_NextRecordset
helpviewer_keywords:
- NextRecordset method [ADO]
ms.assetid: ab1fa449-a695-4987-b1ee-bc68f89418dd
author: rothja
ms.author: jroth
ms.openlocfilehash: 8ec3bb3a6c5f7e4f6d6654ca059e7ace7d97d9da
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443090"
---
# <a name="nextrecordset-method-ado"></a>NextRecordset 方法 (ADO)
清除目前的 [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md) 物件，並藉由前進一系列的命令，傳回下一個 **記錄集** 。  
  
## <a name="syntax"></a>語法  
  
```  
  
Set recordset2 = recordset1.NextRecordset(RecordsAffected )  
```  
  
## <a name="return-value"></a>傳回值  
 傳回 **記錄集** 物件。 在語法模型中， *recordset1* 和 *recordset2* 可以是相同的 **記錄集** 物件，也可以使用不同的物件。 使用不同的**記錄集**物件時，在呼叫**NextRecordset**之後，重設原始**記錄集**上的**ActiveConnection**屬性 (*recordset1*) 將會產生錯誤。  
  
#### <a name="parameters"></a>參數  
 *RecordsAffected*  
 選擇性。 **長**變數，提供者會傳回目前作業受影響的記錄數目。  
  
> [!NOTE]
>  此參數只會傳回受作業影響的記錄數目;它不會從用來產生 **記錄集**的 select 語句傳回記錄的計數。  
  
## <a name="remarks"></a>備註  
 您可以使用 **NextRecordset** 方法，在複合命令語句或傳回多個結果的預存程式中，傳回下一個命令的結果。 如果您根據複合命令語句來開啟**記錄集**物件 (例如 "SELECT \* FROM table1;SELECT \* FROM table2 ") 在[命令](../../../ado/reference/ado-api/command-object-ado.md)上使用[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)方法或在**記錄集**的[Open](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法上，ADO 只會執行第一個命令，並將結果傳回*記錄集*。 若要存取語句中後續命令的結果，請呼叫 **NextRecordset** 方法。  
  
 只要有其他結果，而且包含複合陳述式的 **記錄集** 未在進程界限之間中斷連接或封送處理， **NextRecordset** 方法就會繼續傳回 **記錄集** 物件。 如果傳回資料列的命令順利執行但未傳回任何記錄，則傳回的 **記錄集** 物件將會開啟，但會是空的。 藉由確認 [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 和 [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 屬性都是 **True**來測試此案例。 如果非資料列傳回的命令成功執行，則傳回的**記錄集**物件將會關閉，您可以藉由測試**記錄集**上的[State](../../../ado/reference/ado-api/state-property-ado.md)屬性來進行驗證。 如果沒有其他結果，則會將 *記錄集* 設定為 *Nothing*。  
  
 **NextRecordset**方法無法在已中斷連線的**記錄集**物件上使用，其中[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)已設定為 Microsoft Visual Basic) 中的**Nothing** (或其他語言) 中的 Null (。  
  
 如果在立即更新模式中進行編輯，則呼叫 **NextRecordset** 方法會產生錯誤;先呼叫 [Update](../../../ado/reference/ado-api/update-method.md) 或 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) 方法。  
  
 若要藉由填滿 [參數](../../../ado/reference/ado-api/parameters-collection-ado.md) 集合或傳遞具有原始 **Open** 或 **Execute** 呼叫的陣列，在複合陳述式中傳遞多個命令的參數，這些參數在集合或陣列中的順序必須與命令系列中各自的命令相同。 您必須在讀取輸出參數值之前，先完成讀取所有結果。  
  
 您的 OLE DB 提供者會決定在複合陳述式中執行每個命令的時間。 例如， [適用于 SQL Server 的 Microsoft OLE DB 提供者](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)會在收到複合陳述式時，執行批次中的所有命令。 當您呼叫**NextRecordset**時，會直接傳回產生的**記錄集**。  
  
 不過，在呼叫 NextRecordset 之後，其他提供者可能只會在語句中執行下一個命令。 對於這些提供者，如果您在逐步執行整個命令語句之前明確關閉 **記錄集** 物件，則 ADO 絕對不會執行其餘的命令。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB) 的 NextRecordset 方法範例 ](../../../ado/reference/ado-api/nextrecordset-method-example-vb.md)   
 [NextRecordset 方法範例 (VC++)](../../../ado/reference/ado-api/nextrecordset-method-example-vc.md)   
