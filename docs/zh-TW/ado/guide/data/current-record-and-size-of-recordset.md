---
title: 目前的記錄和資料錄集的大小 |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- record location [ADO]
- current record [ADO]
ms.assetid: e63ff331-8655-4be7-82c6-e6cd6cc9d16d
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 51407df229debf21a3f841c1e8cf1603b2dc43a6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="current-record-and-size-of-recordset"></a>目前的記錄和資料錄集的大小
本章節描述如何在範例中尋找目前的游標位置**資料錄集**中[JScript 程式碼範例，以傳回一個資料錄集](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md)。  
  
## <a name="current-record"></a>目前的記錄  
 在資料集中目前的記錄對應至所指的游標的位置，**資料錄集**物件。 當**資料錄集**從資料來源傳回物件的呼叫結果**Recordset.Open**， **Command.Execute**，或**Connection.Execute** (包括**Connection.NamedCommand**和**Connection.StoredProcedure**)，資料指標設定為指向第一筆記錄。 在範例資料集的初始的目前記錄是"得以 Bob 有機 Dried 梨子"項目。  
  
## <a name="size-of-recordset"></a>資料錄集的大小  
 若要找出的大小**資料錄集**物件中取得的值**Recordset.RecordCount**屬性。 這個值會指出中的記錄數目的長整數**資料錄集**。 如果 Microsoft SQL server OLEDB 提供者傳回資料集，這個值會提供傳回資料列數目。 讀取**RecordCount**上關閉屬性**資料錄集**會造成錯誤。  
  
 如果無法判別的記錄數目，屬性的值為-1。  
  
 值**RecordCount**屬性也取決於提供者和使用的資料指標類型的功能。 順向資料指標的值是-1。 對於靜態或索引鍵集資料指標，這個值會是記錄中傳回的實際數目**資料錄集**物件。 動態資料指標的值為-1 或實際的記錄數，根據資料來源。  
  
 支援的資料指標**Recordcount**必須工作困難，因此需要更多計算能力的資料指標不支援非**Recordcount**。 如果您不需要知道的記錄數目，使用不同的資料指標類型可能有助於改善應用程式的效能，特別是如果您必須處理大型資料集。  
  
 在某些情況下，提供者或資料指標是無法判斷**RecordCount**不含第一個擷取的所有記錄資料來源的值。 若要確保精確的計算，請呼叫**資料錄集**。**MoveLast**方法之前先呼叫**Recordset.RecordCount**。  
  
 此範例**資料錄集**物件，取得使用[JScript 程式碼範例](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md)使用順向資料指標，因此呼叫**RecordCount**此物件上永遠都會造成-1。 如果您變更呼叫的程式碼行**資料錄集**。**開啟**方法，如下列範例所示**RecordCount**屬性會傳回實際讀取的記錄數目。  
  
```  
oRs.Open sSQL, sCnStr, adOpenStatic, adLockOptimistic, adCmdText   
```  
  
 這是因為靜態資料指標與[Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)支援**RecordCount**。 在此範例中，有五筆記錄，因此**RecordCount**應該產生的值為 5。  
  
 本章節包含下列主題。  
  
 [資料錄集的界限](../../../ado/guide/data/boundaries-of-a-recordset.md)
