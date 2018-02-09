---
title: "交易處理 |Microsoft 文件"
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
helpviewer_keywords:
- transactions [ADO]
- data updates [ADO], transaction processing
- updating data [ADO], transaction processing
- nested transactions [ADO]
ms.assetid: 74ab6706-e2dc-42cb-af77-dbc58a9cf4ce
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c37bf04fd14bb2d5f276efd3321b044759cbe7ee
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="transaction-processing"></a>交易處理
A*交易*分隔的開頭和結尾的一系列在連線之間執行資料存取作業。 資料來源時，交易式功能而定**連接**物件也可讓您建立及管理交易。 例如，使用 Microsoft OLE DB Provider for SQL Server 存取 Microsoft SQL Server 上的資料庫，您就可以建立多個巢狀的交易，您所執行的命令。  
  
 ADO 可確保成功一起或完全無法執行，會發生交易中的作業所產生的資料來源的變更。  
  
 如果您取消交易，或其中一個作業失敗，結果會如同沒有任何作業在交易中發生。 資料來源將仍維持交易開始之前。  
  
 ADO 提供下列方法來控制交易： **BeginTrans**， **CommitTrans**，和**RollbackTrans**。 使用這些方法可搭配**連接**物件時，您想要儲存或取消一系列當做單一單位的來源資料所做的變更。 例如，若要傳輸之間帳戶的金錢，您減去某數從其中一個，並將相同的數量，加入另。 如果是更新失敗時，帳戶不再之間取得平衡。 進行這些變更開啟的交易內時，可確保所有或任何的變更移。  
  
> [!NOTE]
>  並非所有提供者支援交易。 確認提供者定義的屬性"**交易 DDL**"會出現在**連接**物件的[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合，表示提供者支援交易。 如果提供者不支援交易，則呼叫其中一種方法會傳回錯誤。  
  
 在您呼叫後**BeginTrans**方法，提供者將不會再立即認可的變更，直到您呼叫您進行**CommitTrans**或**RollbackTrans**結束交易。  
  
 呼叫**CommitTrans**方法會儲存在連接上開啟的交易內進行變更並結束交易。 呼叫**RollbackTrans**方法復原任何開啟的交易內進行的變更並結束交易。 呼叫其中一個方法，沒有開啟的交易時，會產生錯誤。  
  
 取決於**連接**物件的[屬性](../../../ado/reference/ado-api/attributes-property-ado.md)屬性，呼叫**CommitTrans**或**RollbackTrans**方法可能自動啟動新交易。 如果**屬性**屬性設定為**adXactCommitRetaining**，提供者會自動啟動新的交易後**CommitTrans**呼叫。 如果**屬性**屬性設定為**adXactAbortRetaining**，提供者會自動啟動新的交易後**RollbackTrans**呼叫。  
  
## <a name="transaction-isolation-level"></a>交易隔離等級  
 使用**IsolationLevel**屬性上設定交易的隔離等級**連接**物件。 設定不會不會生效，直到您呼叫在下一次[BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)方法。 如果您要求的隔離層級無法使用，提供者可能會傳回下一個更高的隔離等級。 請參閱**IsolationLevel** ADO 程式設計人員參考，如需有關有效的值中的屬性。  
  
## <a name="nested-transactions"></a>巢狀的交易  
 提供者支援巢狀的交易，呼叫**BeginTrans**開啟的交易內的方法會啟動新的巢狀交易。 傳回值會指出的巢狀層級:"1"的傳回值會指出您已開啟最上層的交易 （也就是交易不巢狀另一個交易內），"2"表示您已開啟第二個層級的交易 (交易巢狀最上層的交易），依此類推。 呼叫**CommitTrans**或**RollbackTrans**影響最最近開啟的交易，則您必須關閉，或復原目前交易之前可以解決任何較高層級的交易。
