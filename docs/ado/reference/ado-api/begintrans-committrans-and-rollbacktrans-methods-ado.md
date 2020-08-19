---
description: BeginTrans、CommitTrans 和 RollbackTrans 方法 (ADO)
title: " (ADO) 的 BeginTrans、CommitTrans 和 RollbackTrans 方法 |Microsoft Docs"
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 71dd02544e80d24e96d9cc64fa1e5947f38c685a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451190"
---
# <a name="begintrans-committrans-and-rollbacktrans-methods-ado"></a>BeginTrans、CommitTrans 和 RollbackTrans 方法 (ADO)
這些交易方法會管理 [連接](../../../ado/reference/ado-api/connection-object-ado.md) 物件內的交易處理，如下所示：  
  
-   **BeginTrans** 開始新的交易。  
  
-   **CommitTrans** 儲存任何變更並結束目前的交易。 它也可以啟動新的交易。  
  
-   **RollbackTrans** 取消目前交易期間所做的任何變更，並結束交易。 它也可以啟動新的交易。  
  
## <a name="syntax"></a>語法  
  
```  
  
level = object.BeginTrans()  
object.BeginTrans  
object.CommitTrans  
object.RollbackTrans  
```  
  
## <a name="return-value"></a>傳回值  
 **BeginTrans** 可以被呼叫為函式，以傳回指出交易之嵌套層級的 **長** 變數。  
  
#### <a name="parameters"></a>參數  
 *object*  
 **連接**物件。  
  
## <a name="connection"></a>Connection  
 當您想要以單一單位儲存或取消一系列對來源資料所做的變更時，請使用這些方法搭配 **連接** 物件。 例如，若要在帳戶之間傳輸金額，您可以從1減去數量，並將相同的金額新增至另一個。 如果其中一項更新失敗，帳戶就不會再進行平衡。 在開放式交易內進行這些變更，可確保所有或全部變更都不會通過。  
  
> [!NOTE]
>  並非所有提供者都支援交易。 確認提供者定義的屬性「**交易 DDL**」出現在 **連接** 物件的 [屬性](../../../ado/reference/ado-api/properties-collection-ado.md) 集合中，指出提供者支援交易。 如果提供者不支援交易，則呼叫其中一個方法將會傳回錯誤。  
  
 在您呼叫 **BeginTrans** 方法之後，提供者將無法立即認可您所做的變更，直到您呼叫 **CommitTrans** 或 **RollbackTrans** 來結束交易為止。  
  
 針對支援嵌套交易的提供者，呼叫開放式交易內的 **BeginTrans** 方法會啟動新的嵌套交易。 傳回值表示嵌套層級： "1" 的傳回值表示您已開啟最上層交易 (也就是交易未在另一個交易內進行嵌套) 「2」表示您已開啟第二層交易 (在最上層交易中嵌套的交易) 等等。 呼叫 **CommitTrans** 或 **RollbackTrans** 只會影響最近開啟的交易;您必須先關閉或復原目前的交易，才能解決任何較高層級的交易。  
  
 呼叫 **CommitTrans** 方法會儲存在連接上的開啟交易中所做的變更，並結束交易。 呼叫 **RollbackTrans** 方法會反轉在開啟的交易內進行的任何變更，並結束交易。 沒有開啟的交易時，呼叫任一方法會產生錯誤。  
  
 根據 **連接** 物件的 [屬性](../../../ado/reference/ado-api/attributes-property-ado.md) 屬性，呼叫 **CommitTrans** 或 **RollbackTrans** 方法可能會自動啟動新的交易。 如果 [ **屬性** ] 屬性設定為 [ **adXactCommitRetaining**]，則提供者會在 **CommitTrans** 呼叫之後自動啟動新的交易。 如果 [ **屬性** ] 屬性設定為 [ **adXactAbortRetaining**]，則提供者會在 **RollbackTrans** 呼叫之後自動啟動新的交易。  
  
## <a name="remote-data-service"></a>遠端資料服務  
 用戶端**連接**物件上無法使用**BeginTrans**、 **CommitTrans**和**RollbackTrans**方法。  
  
## <a name="applies-to"></a>套用至  
 [Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [BeginTrans、CommitTrans 和 RollbackTrans 方法範例 (VB) ](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [BeginTrans、CommitTrans 和 RollbackTrans 方法範例 (VC + +) ](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vc.md)   
 [Attributes 屬性 (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
