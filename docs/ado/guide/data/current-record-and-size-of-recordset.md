---
description: 目前的記錄和資料錄集的大小
title: 目前記錄和記錄集的大小 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record location [ADO]
- current record [ADO]
ms.assetid: e63ff331-8655-4be7-82c6-e6cd6cc9d16d
author: rothja
ms.author: jroth
ms.openlocfilehash: 3f7001bb1c53f126498cd94878e02ae8b539ef68
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991489"
---
# <a name="current-record-and-size-of-recordset"></a>目前的記錄和資料錄集的大小
本節說明如何在 JScript 程式碼範例的範例 **記錄集中** 找出資料指標的目前位置 [，以傳回記錄集](./jscript-code-example-to-return-a-recordset.md)。  
  
## <a name="current-record"></a>目前記錄  
 資料集中的目前記錄會對應至 **記錄集** 物件的資料指標位置所指向的記錄。 當 **記錄集** 物件從資料來源傳回做為呼叫 **記錄集**的結果時，請開啟、 **Command.Exe刻意**或 **Connection.Exe** 的 (包含 **NamedCommand** 和 **StoredProcedure**) ，資料指標會設定為指向第一筆記錄。 在範例資料集中，初始目前的記錄是 "圖報 Bob 的有機蒙娜 Pears" 專案。  
  
## <a name="size-of-recordset"></a>記錄集的大小  
 若要找出 **記錄集** 物件的大小，請取得 **RecordCount** 屬性的值。 這個值是長整數，表示記錄 **集**內的記錄數目。 如果從 Microsoft SQL Server 的 OLEDB 提供者傳回資料集，此值會提供傳回的資料列數目。 讀取已關閉**記錄集**上的**RecordCount**屬性會導致錯誤。  
  
 如果無法判斷記錄數目，則屬性的值為-1。  
  
 **RecordCount**屬性的值也取決於提供者的功能和使用的資料指標類型。 如果是順向資料指標，此值為-1。 若為靜態或索引鍵集資料指標，此值會是 **記錄集** 物件中傳回的實際記錄數目。 若為動態資料指標，此值為-1 或實際的記錄數目（視資料來源而定）。  
  
 支援 **Recordcount** 的資料指標必須較難處理，因此需要更多運算能力，而不是資料指標不支援 **Recordcount**。 如果您不需要知道記錄的數目，則使用不同的資料指標類型可能有助於改善應用程式的效能，特別是當您必須處理大型資料集時。  
  
 在某些情況下，提供者或資料指標無法先從資料來源提取所有記錄，而無法判斷 **RecordCount** 值。 若要確保正確的計數，請呼叫**記錄集**。呼叫**記錄集之前的** **MoveLast**方法 RecordCount。  
  
 使用[JScript 程式碼範例](./jscript-code-example-to-return-a-recordset.md)取得的範例**記錄集**物件會使用順向資料指標，因此在此物件上呼叫**RecordCount**一律會產生-1。 如果您變更呼叫 **記錄集**的程式程式碼。**Open** 方法如下列範例所示， **RecordCount** 屬性會傳回實際提取的記錄數目。  
  
```  
oRs.Open sSQL, sCnStr, adOpenStatic, adLockOptimistic, adCmdText   
```  
  
 這是因為具有 [Microsoft OLE DB Provider for SQL Server](../appendixes/microsoft-ole-db-provider-for-sql-server.md) 支援 **RecordCount**的靜態資料指標。 在此範例中，有五筆記錄，因此 **RecordCount** 應該產生5的值。  
  
 本節包含下列主題。  
  
 [資料錄集的界限](./boundaries-of-a-recordset.md)