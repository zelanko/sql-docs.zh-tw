---
title: BeginTrans、 CommitTrans 和 RollbackTrans 方法 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::raw_RollbackTrans
- Connection15::CommitTrans
- Connection15::raw_CommitTrans
- Connection15::raw_BeginTrans
- Connection15::BeginTrans
- Connection15::RollbackTrans
helpviewer_keywords:
- BeginTrans method [ADO]
- CommitTrans method [ADO]
- RollbackTrans method [ADO]
ms.assetid: d4683472-4120-4236-8640-fa9ae289e23e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ee5560a27f7df49a82e964753f792bd46270d3a6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66696490"
---
# <a name="begintrans-committrans-and-rollbacktrans-methods-ado"></a>BeginTrans、CommitTrans 和 RollbackTrans 方法 (ADO)
這些交易方法管理內處理的交易[連線](../../../ado/reference/ado-api/connection-object-ado.md)物件，如下所示：  
  
-   **BeginTrans**開始新交易。  
  
-   **CommitTrans**儲存任何變更，並結束目前的交易。 它也可以啟動新的交易。  
  
-   **RollbackTrans**取消任何目前的交易期間所做的變更並結束交易。 它也可以啟動新的交易。  
  
## <a name="syntax"></a>語法  
  
```  
  
level = object.BeginTrans()  
object.BeginTrans  
object.CommitTrans  
object.RollbackTrans  
```  
  
## <a name="return-value"></a>傳回值  
 **BeginTrans**傳回的函式可以呼叫**長**變數，表示交易的巢狀層級。  
  
#### <a name="parameters"></a>參數  
 *object*  
 A**連線**物件。  
  
## <a name="connection"></a>連接  
 使用這些方法可搭配**連線**物件時您想要儲存或取消一系列的當做單一單位的來源資料所做的變更。 比方說，帳戶之間傳輸金錢，您減去從某個量，並新增相同數量之間。 如果其中一個更新失敗時，帳戶不再之間取得平衡。 進行這些變更，在開啟的交易內，可確保所有或的任何變更，瀏覽。  
  
> [!NOTE]
>  並非所有提供者支援交易。 確認提供者定義的屬性"**交易 DDL**"會出現在**連線**物件的[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合，表示提供者支援交易。 如果提供者不支援交易，呼叫其中一個方法會傳回錯誤。  
  
 在您呼叫後**BeginTrans**方法，提供者將不會再立即認可直到您呼叫您所做的變更**CommitTrans**或是**RollbackTrans**結束交易。  
  
 提供者支援巢狀的交易，呼叫**BeginTrans**開啟的交易內的方法會啟動新的巢狀交易。 傳回值，表示巢狀層級:"1"的傳回值會指出您已開啟的最上層的交易 （也就是交易不巢狀在另一個交易內），"2"表示您已開啟第二個層級交易 (交易巢狀結構最上層的交易內），依此類推。 呼叫**CommitTrans**或是**RollbackTrans**影響只有最最近開啟的交易，您必須關閉，或回復目前交易之前，您可以解決任何較高層級的交易。  
  
 呼叫**CommitTrans**方法會儲存在連接上開啟的交易內進行變更並結束交易。 呼叫**RollbackTrans**方法會反轉任何開啟的交易內所做的變更並結束交易。 呼叫任一方法，沒有任何開啟的交易時，會產生錯誤。  
  
 取決於**連接**物件的[屬性](../../../ado/reference/ado-api/attributes-property-ado.md)屬性，呼叫**CommitTrans**或是**RollbackTrans**方法可能自動啟動新的交易。 如果**屬性**屬性設定為**adXactCommitRetaining**，提供者會自動啟動新的交易之後**CommitTrans**呼叫。 如果**屬性**屬性設定為**adXactAbortRetaining**，提供者會自動啟動新的交易之後**RollbackTrans**呼叫。  
  
## <a name="remote-data-service"></a>遠端資料服務  
 **BeginTrans**， **CommitTrans**，並**RollbackTrans**方法並不適用於用戶端**連接**物件。  
  
## <a name="applies-to"></a>適用於  
 [Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [BeginTrans、 CommitTrans 和 RollbackTrans 方法範例 (VB)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [BeginTrans、 CommitTrans 和 RollbackTrans 方法範例 （VC + +）](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vc.md)   
 [Attributes 屬性 (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
