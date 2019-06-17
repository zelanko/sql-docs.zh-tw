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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: edd070cc6f10829b597534d024d767de2a0c7e12
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66701715"
---
# <a name="receiving-results"></a>接收結果
在 ADO 中大部分的命令會導致傳回給呼叫端的某些資訊。 如需傳回資料列集的命令，在收到結果**資料錄集**物件，這是可能最常使用之 ADO 物件。  
  
 有數種方式接收中的資料**資料錄集**從資料來源，包括呼叫下列物件：  
  
-   [Connection.Execute 方法](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Command.Execute 方法](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Recordset.Open 方法](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Connection.NamedCommand](../../../ado/guide/data/named-commands.md)  
  
-   [Connection.StoredProcedure](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
 接收中的資料**Recordset**物件到結束的資料，使用的參與程序**連線**物件和**命令**物件，以隱含方式或明確。 在一般的用戶端/伺服器應用程式系統中，取得資料的整個程序需要透過網路來回行程填滿每個**資料錄集**。  
  
 您必須進行幾個方法來接收多個結果集透過網路，其中每個資料集封裝在來回行程**資料錄集**物件。 對於較慢或擁塞的網路，減少往返次數可能有助於改善應用程式的效能。 因此，某些提供者提供支援，以接收多個**資料錄集**單一來回行程。 這是由下列主題所述：  
  
-   [接收多個資料錄集](../../../ado/guide/data/receiving-multiple-recordsets.md)
