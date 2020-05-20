---
title: 目前記錄和記錄集的大小 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 30b669a566270a0eff5d6cf93abb5b0acb7ff3c2
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761124"
---
# <a name="current-record-and-size-of-recordset"></a>目前的記錄和資料錄集的大小
本節說明如何在 JScript 程式碼範例的範例**記錄集中**找出資料指標的目前位置[，以傳回記錄集](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md)。  
  
## <a name="current-record"></a>目前記錄  
 資料集中的目前記錄會對應至**記錄集**物件的游標位置所指向的。 當從資料來源傳回**記錄集**物件做為呼叫**記錄集**的結果時，請開啟、**執行命令**或**連接。 execute** （包括**NamedCommand**和**StoredProcedure**），資料指標會設定為指向第一筆記錄。 在範例資料集中，初始的目前記錄是 "圖報 Bob 的有機蒙娜 Pears" 專案。  
  
## <a name="size-of-recordset"></a>記錄集的大小  
 若要找出**記錄集**物件的大小，請取得**RecordCount**屬性的值。 這個值是長整數，表示記錄**集**內的記錄數目。 如果 Microsoft SQL Server 的 OLEDB 提供者傳回資料集，這個值會提供傳回的資料列數目。 讀取封閉**記錄集**上的**RecordCount**屬性會造成錯誤。  
  
 如果無法判斷記錄的數目，則屬性的值為-1。  
  
 **RecordCount**屬性的值也取決於提供者的功能和所使用的資料指標類型。 若為順向資料指標，此值為-1。 若為靜態或索引鍵集資料指標，此值就是在**記錄集**物件中傳回的實際記錄數目。 若為動態資料指標，此值為-1 或實際的記錄數目，視資料來源而定。  
  
 支援**Recordcount**的資料指標必須更難處理，因此需要更多運算能力，而不是資料指標不支援**Recordcount**。 如果您不需要知道記錄數目，使用不同的資料指標類型可能有助於改善應用程式的效能，特別是當您必須處理大型資料集時。  
  
 在某些情況下，提供者或資料指標無法判斷**RecordCount**值，而不需要先從資料來源提取所有記錄。 若要確保正確的計數，請呼叫**記錄集**。呼叫**記錄集之前的** **MoveLast**方法 RecordCount。  
  
 使用[JScript 程式碼範例](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md)取得的範例**記錄集**物件會使用順向資料指標，因此在此物件上呼叫**RecordCount**一律會產生-1。 如果您變更呼叫**記錄集**的程式程式碼。**Open**方法如下列範例所示， **RecordCount**屬性會傳回所提取的實際記錄數目。  
  
```  
oRs.Open sSQL, sCnStr, adOpenStatic, adLockOptimistic, adCmdText   
```  
  
 這是因為具有[Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)支援**RecordCount**的靜態資料指標。 在此範例中，有五個記錄，因此**RecordCount**應該會產生5的值。  
  
 本章節包含下列主題。  
  
 [資料錄集的界限](../../../ado/guide/data/boundaries-of-a-recordset.md)
