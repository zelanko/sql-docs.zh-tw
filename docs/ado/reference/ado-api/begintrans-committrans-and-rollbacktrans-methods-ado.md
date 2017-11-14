---
title: "BeginTrans、 CommitTrans 和 RollbackTrans 方法 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
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
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3e973503fcdd7a524bab21364428be6b955017af
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="begintrans-committrans-and-rollbacktrans-methods-ado"></a>BeginTrans、 CommitTrans 和 RollbackTrans 方法 (ADO)
這些交易方法管理交易中處理[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件，如下所示：  
  
-   **BeginTrans**開始新交易。  
  
-   **CommitTrans**儲存任何變更，並結束目前的交易。 它也可能會啟動新交易。  
  
-   **RollbackTrans**取消任何目前的交易期間所做的變更並結束交易。 它也可能會啟動新交易。  
  
## <a name="syntax"></a>語法  
  
```  
  
level = object.BeginTrans()  
object.BeginTrans  
object.CommitTrans  
object.RollbackTrans  
```  
  
## <a name="return-value"></a>傳回值  
 **BeginTrans**可以做為傳回的函式呼叫**長**變數，表示交易的巢狀層級。  
  
#### <a name="parameters"></a>參數  
 *物件*  
 A**連接**物件。  
  
## <a name="connection"></a>連接  
 使用這些方法可搭配**連接**物件時，您想要儲存或取消一系列當做單一單位的來源資料所做的變更。 例如，若要傳輸之間帳戶的金錢，您減去某數從其中一個，並將相同的數量，加入另。 如果是更新失敗時，帳戶不再之間取得平衡。 進行這些變更開啟的交易內時，可確保所有或任何的變更移。  
  
> [!NOTE]
>  並非所有提供者支援交易。 確認提供者定義的屬性"**交易 DDL**"會出現在**連接**物件的[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合，表示提供者支援交易。 如果提供者不支援交易，則呼叫其中一種方法會傳回錯誤。  
  
 在您呼叫後**BeginTrans**方法，提供者將不會再立即認可的變更，直到您呼叫您進行**CommitTrans**或**RollbackTrans**結束交易。  
  
 提供者支援巢狀的交易，呼叫**BeginTrans**開啟的交易內的方法會啟動新的巢狀交易。 傳回值會指出的巢狀層級:"1"的傳回值會指出您已開啟最上層的交易 （也就是交易不巢狀另一個交易內），"2"表示您已開啟第二個層級的交易 (交易巢狀最上層的交易），依此類推。 呼叫**CommitTrans**或**RollbackTrans**影響最最近開啟的交易，則您必須關閉，或復原目前交易之前可以解決任何較高層級的交易。  
  
 呼叫**CommitTrans**方法會儲存在連接上開啟的交易內進行變更並結束交易。 呼叫**RollbackTrans**方法復原任何開啟的交易內進行的變更並結束交易。 呼叫其中一個方法，沒有開啟的交易時，會產生錯誤。  
  
 取決於**連接**物件的[屬性](../../../ado/reference/ado-api/attributes-property-ado.md)屬性，呼叫**CommitTrans**或**RollbackTrans**方法可能自動啟動新交易。 如果**屬性**屬性設定為**adXactCommitRetaining**，提供者會自動啟動新的交易後**CommitTrans**呼叫。 如果**屬性**屬性設定為**adXactAbortRetaining**，提供者會自動啟動新的交易後**RollbackTrans**呼叫。  
  
## <a name="remote-data-service"></a>遠端資料服務  
 **BeginTrans**， **CommitTrans**，和**RollbackTrans**方法不會提供用戶端**連接**物件。  
  
## <a name="applies-to"></a>適用於  
 [連接物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [BeginTrans、 CommitTrans 和 RollbackTrans 方法範例 (VB)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [BeginTrans、 CommitTrans 和 RollbackTrans 方法範例 （VC + +）](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vc.md)   
 [屬性的內容 (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)

