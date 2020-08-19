---
description: 交易處理
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 5b4d8e959cab799c5436b1c1357ae1e734d3d5a0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452700"
---
# <a name="transaction-processing"></a>交易處理
*交易*分隔一系列在連接上執行的資料存取作業的開頭和結尾。 以您資料來源的交易式功能為依據， **連接** 物件也可讓您建立和管理交易。 例如，使用適用于 SQL Server 的 Microsoft OLE DB 提供者存取 Microsoft SQL Server 上的資料庫時，您可以為執行的命令建立多個嵌套交易。  
  
 ADO 可確保對交易中的作業所產生的資料來源所做的變更，會成功地一起發生。  
  
 如果您取消交易，或其中一個作業失敗，則結果將會和交易中沒有任何作業發生一樣。 資料來源將維持在交易開始之前的狀態。  
  
 ADO 提供下列方法來控制交易： **BeginTrans**、 **CommitTrans**和 **RollbackTrans**。 當您想要以單一單位儲存或取消一系列對來源資料所做的變更時，請使用這些方法搭配 **連接** 物件。 例如，若要在帳戶之間傳輸金額，您可以從1減去數量，並將相同的金額新增至另一個。 如果其中一項更新失敗，帳戶就不會再進行平衡。 在開放式交易內進行這些變更，可確保所有或全部變更都不會通過。  
  
> [!NOTE]
>  並非所有提供者都支援交易。 確認提供者定義的屬性「**交易 DDL**」出現在 **連接** 物件的 [屬性](../../../ado/reference/ado-api/properties-collection-ado.md) 集合中，指出提供者支援交易。 如果提供者不支援交易，則呼叫其中一個方法將會傳回錯誤。  
  
 在您呼叫 **BeginTrans** 方法之後，提供者將無法立即認可您所做的變更，直到您呼叫 **CommitTrans** 或 **RollbackTrans** 來結束交易為止。  
  
 呼叫 **CommitTrans** 方法會儲存在連接上的開啟交易中所做的變更，並結束交易。 呼叫 **RollbackTrans** 方法會反轉在開啟的交易內進行的任何變更，並結束交易。 沒有開啟的交易時，呼叫任一方法會產生錯誤。  
  
 根據 **連接** 物件的 [屬性](../../../ado/reference/ado-api/attributes-property-ado.md) 屬性，呼叫 **CommitTrans** 或 **RollbackTrans** 方法可能會自動啟動新的交易。 如果 [ **屬性** ] 屬性設定為 [ **adXactCommitRetaining**]，則提供者會在 **CommitTrans** 呼叫之後自動啟動新的交易。 如果 [ **屬性** ] 屬性設定為 [ **adXactAbortRetaining**]，則提供者會在 **RollbackTrans** 呼叫之後自動啟動新的交易。  
  
## <a name="transaction-isolation-level"></a>交易隔離等級  
 您可以使用 **IsolationLevel** 屬性，在 **連接** 物件上設定交易的隔離等級。 除非您下一次呼叫 [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) 方法，否則設定不會生效。 如果您要求的隔離層級無法使用，則提供者可能會傳回下一個較高層級的隔離。 如需有效值的詳細資訊，請參閱 ADO 程式設計人員參考中的 **IsolationLevel** 屬性。  
  
## <a name="nested-transactions"></a>嵌套交易  
 針對支援嵌套交易的提供者，呼叫開放式交易內的 **BeginTrans** 方法會啟動新的嵌套交易。 傳回值表示嵌套層級： "1" 的傳回值表示您已開啟最上層交易 (也就是交易未在另一個交易內進行嵌套) 「2」表示您已開啟第二層交易 (在最上層交易中嵌套的交易) 等等。 呼叫 **CommitTrans** 或 **RollbackTrans** 只會影響最近開啟的交易;您必須先關閉或復原目前的交易，才能解決任何較高層級的交易。
