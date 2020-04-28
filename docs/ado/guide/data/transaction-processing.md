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
ms.openlocfilehash: cab6638704856baf873274807c0e2eff9a1f92d8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67923866"
---
# <a name="transaction-processing"></a>交易處理
*交易*會分隔在連接上執行的一系列資料存取作業的開始和結束。 取決於資料來源的交易式功能， **Connection**物件也可讓您建立和管理交易。 例如，使用適用于 SQL Server 的 Microsoft OLE DB 提供者存取 Microsoft SQL Server 上的資料庫時，您可以為執行的命令建立多個嵌套的交易。  
  
 ADO 可確保交易中的作業所產生之資料來源的變更成功地一起發生，或是完全不進行。  
  
 如果您取消交易，或其中一個作業失敗，則結果會與交易中的作業都不會發生。 資料來源會保留在交易開始之前。  
  
 ADO 提供下列方法來控制交易： **BeginTrans**、 **CommitTrans**和**RollbackTrans**。 當您想要以單一單位儲存或取消一系列對來源資料所做的變更時，請將這些方法與**連接**物件搭配使用。 例如，若要在帳戶之間轉移 money，您可以將金額減一，並將相同的金額加到另一個。 如果其中一個更新失敗，則帳戶不會再進行平衡。 在開啟的交易內進行這些變更，可確保所有變更都不會通過。  
  
> [!NOTE]
>  並非所有提供者都支援交易。 確認提供者定義的屬性 "**TRANSACTION DDL**" 出現在**Connection**物件的[Properties](../../../ado/reference/ado-api/properties-collection-ado.md)集合中，表示該提供者支援交易。 如果提供者不支援交易，則呼叫其中一個方法將會傳回錯誤。  
  
 在您呼叫**BeginTrans**方法之後，提供者將不會再立即認可您所做的變更，直到您呼叫**CommitTrans**或**RollbackTrans**結束交易為止。  
  
 呼叫**CommitTrans**方法會儲存在連接上開啟的交易內所做的變更，並結束交易。 呼叫**RollbackTrans**方法會反轉在開啟的交易內所做的任何變更，並結束交易。 當沒有開啟的交易時呼叫任一方法會產生錯誤。  
  
 根據**連接**物件的 [[屬性](../../../ado/reference/ado-api/attributes-property-ado.md)] 屬性，呼叫**CommitTrans**或**RollbackTrans**方法可能會自動啟動新的交易。 如果 [**屬性**] 屬性設為**adXactCommitRetaining**，則提供者會在**CommitTrans**呼叫之後自動啟動新的交易。 如果 [**屬性**] 屬性設為**adXactAbortRetaining**，則提供者會在**RollbackTrans**呼叫之後自動啟動新的交易。  
  
## <a name="transaction-isolation-level"></a>交易隔離等級  
 使用**IsolationLevel**屬性，即可設定**連接**物件上交易的隔離等級。 在下一次呼叫[BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)方法之前，設定不會生效。 如果您要求的隔離層級無法使用，提供者可能會傳回下一個較高層級的隔離。 如需有效值的詳細資訊，請參閱 ADO 程式設計人員參考中的**IsolationLevel**屬性。  
  
## <a name="nested-transactions"></a>嵌套交易  
 對於支援嵌套交易的提供者，在開啟的交易內呼叫**BeginTrans**方法會啟動新的、嵌套的交易。 傳回值會指出嵌套的層級：傳回值 "1" 表示您已開啟最上層交易（也就是交易未在另一個交易中嵌套），"2" 表示您已開啟第二層交易（在最上層交易內的交易），依此類推。 呼叫**CommitTrans**或**RollbackTrans**只會影響最近開啟的交易;您必須先關閉或回復目前的交易，才能解決任何較高層級的交易。
