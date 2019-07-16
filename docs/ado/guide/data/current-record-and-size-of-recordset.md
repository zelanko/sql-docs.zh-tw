---
title: 目前的記錄和資料錄集的大小 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record location [ADO]
- current record [ADO]
ms.assetid: e63ff331-8655-4be7-82c6-e6cd6cc9d16d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a01e17ea9c786a724e5869a28bf4d8927b58ac81
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925698"
---
# <a name="current-record-and-size-of-recordset"></a>目前的記錄和資料錄集的大小
本章節描述如何在此範例中找出目前的游標位置**Recordset**中[JScript 程式碼範例，以傳回資料錄集](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md)。  
  
## <a name="current-record"></a>目前的記錄  
 資料集的目前資料錄對應至所指的資料指標的位置，**資料錄集**物件。 當**Recordset**物件時，會傳回資料來源上，呼叫的結果做**Recordset.Open**， **Command.Execute**，或**Connection.Execute** (包括**Connection.NamedCommand**並**Connection.StoredProcedure**)，資料指標設定為指向第一筆記錄。 範例資料集，在初始的目前資料錄會是"得以 Bob 有機 Dried 梨子"項目。  
  
## <a name="size-of-recordset"></a>資料錄集的大小  
 若要了解的大小**Recordset**物件，取得的值**Recordset.RecordCount**屬性。 這個值是表示中的記錄數目的長整數**資料錄集**。 如果 Microsoft SQL server OLEDB 提供者傳回資料集，這個值會提供傳回資料列數目。 讀取**RecordCount**屬性已關閉**資料錄集**會造成錯誤。  
  
 如果無法判別的記錄數目，則屬性的值為-1。  
  
 值**RecordCount**屬性也取決於提供者使用的資料指標類型的功能。 順向資料指標的值為-1。 靜態或索引鍵集資料指標的值是記錄中傳回的實際數目**資料錄集**物件。 動態資料指標值會是-1 或記錄，根據資料來源的實際數目。  
  
 支援的資料指標**Recordcount**必須工作，且因此需要更多的運算能力，比在資料指標不支援**Recordcount**。 如果您不需要知道的記錄數目，使用不同的資料指標類型可能有助於改善您的應用程式效能，尤其是如果您必須處理大型資料集。  
  
 在某些情況下，提供者或資料指標是無法判定**RecordCount**不含第一個資料來源中擷取所有記錄值。 若要確保正確計算，請呼叫**Recordset**。**MoveLast**方法之前呼叫**Recordset.RecordCount**。  
  
 範例**Recordset**使用取得的物件[JScript 程式碼範例](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md)使用順向資料指標，因此，呼叫**RecordCount**此物件上永遠會導致-1。 如果您變更程式碼呼叫的一行**Recordset**。**開啟**方法，如下列範例所示**RecordCount**屬性會傳回實際擷取的記錄數目。  
  
```  
oRs.Open sSQL, sCnStr, adOpenStatic, adLockOptimistic, adCmdText   
```  
  
 這是因為靜態資料指標與[Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)支援**RecordCount**。 在此範例中，有五筆記錄，因此**RecordCount**應該產生值為 5。  
  
 本章節包含下列主題。  
  
 [資料錄集的界限](../../../ado/guide/data/boundaries-of-a-recordset.md)
