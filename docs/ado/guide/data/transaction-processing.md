---
title: 交易處理 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- transactions [ADO]
- data updates [ADO], transaction processing
- updating data [ADO], transaction processing
- nested transactions [ADO]
ms.assetid: 74ab6706-e2dc-42cb-af77-dbc58a9cf4ce
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4ea890e0e2d49781f06f38f606a6c92582dc44d1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47742227"
---
# <a name="transaction-processing"></a>交易處理
A*交易*分隔的開頭和結尾的資料存取作業透過連線執行一系列。 資料來源時，交易式功能而定**連線**物件也可讓您建立和管理交易。 例如，若要存取 Microsoft SQL Server 上的資料庫使用 Microsoft OLE DB Provider for SQL Server，您就可以建立您所執行之命令的多個巢狀的交易。  
  
 ADO 可確保已成功在一起或完全不變更資料來源所產生的交易中的作業，會發生。  
  
 如果您取消交易，或其中一個作業失敗，結果會如同沒有任何作業在交易中發生。 交易開始之前，會保留資料來源。  
  
 ADO 提供下列方法來控制交易： **BeginTrans**， **CommitTrans**，並**RollbackTrans**。 使用這些方法可搭配**連線**物件時您想要儲存或取消一系列的當做單一單位的來源資料所做的變更。 比方說，帳戶之間傳輸金錢，您減去從某個量，並新增相同數量之間。 如果其中一個更新失敗時，帳戶不再之間取得平衡。 進行這些變更，在開啟的交易內，可確保所有或的任何變更，瀏覽。  
  
> [!NOTE]
>  並非所有提供者支援交易。 確認提供者定義的屬性"**交易 DDL**"會出現在**連線**物件的[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合，表示提供者支援交易。 如果提供者不支援交易，呼叫其中一個方法會傳回錯誤。  
  
 在您呼叫後**BeginTrans**方法，提供者將不會再立即認可直到您呼叫您所做的變更**CommitTrans**或是**RollbackTrans**結束交易。  
  
 呼叫**CommitTrans**方法會儲存在連接上開啟的交易內進行變更並結束交易。 呼叫**RollbackTrans**方法會反轉任何開啟的交易內所做的變更並結束交易。 呼叫任一方法，沒有任何開啟的交易時，會產生錯誤。  
  
 取決於**連接**物件的[屬性](../../../ado/reference/ado-api/attributes-property-ado.md)屬性，呼叫**CommitTrans**或是**RollbackTrans**方法可能自動啟動新的交易。 如果**屬性**屬性設定為**adXactCommitRetaining**，提供者會自動啟動新的交易之後**CommitTrans**呼叫。 如果**屬性**屬性設定為**adXactAbortRetaining**，提供者會自動啟動新的交易之後**RollbackTrans**呼叫。  
  
## <a name="transaction-isolation-level"></a>交易隔離等級  
 使用**IsolationLevel**屬性上設定交易的隔離等級**連線**物件。 設定不會不會生效，直到您呼叫在下一次[BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)方法。 如果您要求的隔離層級無法使用，提供者可能會傳回下一個更高的隔離等級。 請參閱**IsolationLevel** ADO 程式設計人員參考，如需詳細資訊，有效的值中的屬性。  
  
## <a name="nested-transactions"></a>巢狀的交易  
 提供者支援巢狀的交易，呼叫**BeginTrans**開啟的交易內的方法會啟動新的巢狀交易。 傳回值，表示巢狀層級:"1"的傳回值會指出您已開啟的最上層的交易 （也就是交易不巢狀在另一個交易內），"2"表示您已開啟第二個層級交易 (交易巢狀結構最上層的交易內），依此類推。 呼叫**CommitTrans**或是**RollbackTrans**影響只有最最近開啟的交易，您必須關閉，或回復目前交易之前，您可以解決任何較高層級的交易。
