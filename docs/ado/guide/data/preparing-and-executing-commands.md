---
title: 準備和執行命令 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Command object [ADO], preparing and executing commands
ms.assetid: 7448d9ee-7f4b-47e3-be54-2df8c9bbac32
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2295d421f8b802f2f3b531d7de3fc086e43ad572
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67924567"
---
# <a name="preparing-and-executing-commands"></a>準備和執行命令
命令是對提供者發出的指示，可對基礎資料來源執行某些作業。 例如，SQL 語句是 Microsoft SQL Data Provider 的命令。 在 ADO 中，命令通常是由**Command**物件表示，雖然簡單的命令也可以透過**連接**或**記錄集**物件來發行。  
  
 您可以使用**Command**物件向提供者要求任何支援的作業類型，假設提供者可以正確解讀命令字串。 資料提供者的常見作業是查詢資料庫，並在**記錄集**物件中傳回記錄，這可以被視為容器來保存結果，並使用工具來查看結果。 如同許多 ADO 物件，某些**命令**物件集合、方法或屬性可能會在參考時產生錯誤，視提供者的功能而定。  
  
 除了使用**Command**物件之外，您還可以在**Connection**物件或**Recordset**物件上的**Open**方法上使用**Execute**方法，以發出命令並執行它。 不過，如果您需要在程式碼中重複使用命令，或如果您需要使用命令傳遞詳細的參數資訊，您應該使用**命令**物件。 本章節稍後會詳細說明這些案例。  
  
> [!NOTE]
>  某些**命令**可以將結果集當做二進位資料流程或單一**記錄**（而不是**記錄集**）傳回，如果提供者支援這種情況。 此外，某些**命令**並不打算傳回任何結果集（例如，SQL Update 查詢）。 這一節將涵蓋最常見的案例，不過：執行**命令**會以**記錄集**物件的形式傳回結果。 如需將結果傳回至**記錄**s 或**資料流程**的詳細資訊，請參閱[記錄和資料流程](../../../ado/guide/data/records-and-streams.md)。  
  
 此章節包含下列主題。  
  
-   [Command 物件概觀](../../../ado/guide/data/command-object-overview.md)  
  
-   [建立和執行簡單的命令](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Command 物件參數](../../../ado/guide/data/command-object-parameters.md)  
  
-   [使用命令呼叫預存程序](../../../ado/guide/data/calling-a-stored-procedure-with-a-command.md)  
  
-   [呼叫預存程式做為連線物件上的方法](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
-   [具名命令](../../../ado/guide/data/named-commands.md)  
  
-   [傳遞參數給具名命令](../../../ado/guide/data/passing-parameters-to-a-named-command.md)
