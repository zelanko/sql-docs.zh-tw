---
title: "接收結果 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- receiving results [ADO]
- Recordset object [ADO], receiving results
ms.assetid: 791aa26e-7aae-477e-9f05-5cd46e1de095
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5768404342f76eb8c5999678e6c1a4aa4a3bcd42
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="receiving-results"></a>接收的結果
在 ADO 的大部分命令會傳回呼叫端的一些資訊。 傳回資料列集的命令，在收到結果**資料錄集**物件，這是可能最常使用的 ADO 物件。  
  
 有數種方法來接收資料**資料錄集**來自資料來源，包括呼叫下列物件：  
  
-   [Connection.Execute 方法](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Command.Execute 方法](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Recordset.Open 方法](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Connection.NamedCommand](../../../ado/guide/data/named-commands.md)  
  
-   [Connection.StoredProcedure](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
 接收中的資料**資料錄集**物件結束時，取得資料，以參與的程序**連接**物件和**命令**物件，以隱含方式或明確。 在一般用戶端/伺服器應用程式系統中，取得資料的整個程序需要透過網路往返填入每個**資料錄集**。  
  
 若要接收多個結果集表示您會需要進行數往返透過網路，其中每個資料集封裝在**資料錄集**物件。 慢或壅塞網路減少往返次數可能有助於改善應用程式的效能。 因此，有些提供者會提供支援，以接收多個**資料錄集**s 至單一反覆存取。 這是將討論下列主題：  
  
-   [接收多個資料錄集](../../../ado/guide/data/receiving-multiple-recordsets.md)

