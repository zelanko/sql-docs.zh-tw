---
description: 接收結果
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
ms.openlocfilehash: 3317441322d0f1be94ee1c897946d83f6291143c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452990"
---
# <a name="receiving-results"></a>接收結果
在 ADO 中，大部分的命令會導致某些資訊傳回給呼叫端。 針對傳回資料列集的命令，結果會在 **記錄集** 物件中接收，這可能是 ADO 物件最常使用的結果。  
  
 有數種方式可從資料來源接收 **記錄集** 物件中的資料，包括呼叫下列各項：  
  
-   [Connection.Exe刻意的方法](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Command.Exe刻意的方法](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Recordset. Open 方法](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [連接。 NamedCommand](../../../ado/guide/data/named-commands.md)  
  
-   [連接。 StoredProcedure](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
 以隱含或明確的方式，在 **記錄集** 物件中接收資料，結束取得資料的程式，以及 **連接** 物件和 **命令** 物件的參與。 在一般的用戶端/伺服器應用程式系統中，取得資料的整個程式都需要在網路上針對每個填滿的 **記錄集**進行來回行程。  
  
 若要接收一個以上的結果集，您必須透過網路進行數個往返，每個封裝在 **記錄集** 物件中的資料集都有一個。 對於低速或擁塞的網路，減少往返次數可能有助於改善應用程式的效能。 因此，某些提供者會提供支援，以在單一往返中接收多個 **記錄集**。 下列主題將討論這一點：  
  
-   [接收多個資料錄集](../../../ado/guide/data/receiving-multiple-recordsets.md)
