---
title: 接收結果 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- receiving results [ADO]
- Recordset object [ADO], receiving results
ms.assetid: 791aa26e-7aae-477e-9f05-5cd46e1de095
author: rothja
ms.author: jroth
ms.openlocfilehash: 0e05bd86b908c8c6d7ac08525e425333d3e2f1ad
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759094"
---
# <a name="receiving-results"></a>接收結果
在 ADO 中，大部分的命令會導致某些資訊傳回給呼叫者。 對於傳回資料列集的命令，結果會在**記錄集**物件中收到，這可能是最常使用的 ADO 物件。  
  
 有數種方式可從資料來源接收**記錄集**物件中的資料，包括呼叫下列各項：  
  
-   [Connection. Execute 方法](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [命令. Execute 方法](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [記錄集. Open 方法](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [連接。 NamedCommand](../../../ado/guide/data/named-commands.md)  
  
-   [連接。 StoredProcedure](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
 接收**記錄集**物件中的資料時，會以隱含或明確的方式參與**連接**物件和**命令**物件，以取得資料的處理常式。 在一般的用戶端/伺服器應用程式系統中，取得資料的整個程式都需要透過網路來回行程，以取得每個已填滿的**記錄集**。  
  
 若要接收一個以上的結果集，表示您需要對網路進行數次來回行程，每個資料集都是在**記錄集**物件中封裝的。 針對速度緩慢或擁塞的網路，減少來回行程的次數可能有助於改善應用程式的效能。 因此，某些提供者會提供支援，以在單一往返期間接收多個**記錄集**。 這會在下列主題中討論：  
  
-   [接收多個資料錄集](../../../ado/guide/data/receiving-multiple-recordsets.md)
