---
title: SQLXML 4.0 中的 Diffgram 簡介 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotations [SQLXML]
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: 1902d67f-baf3-46e6-a36c-b24b5ba6f8ea
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 2de8eaa81c5a2e903be2f9bd608c6ccca703718d
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82703137"
---
# <a name="introduction-to-diffgrams-in-sqlxml-40"></a>DiffGrams 的 SQLXML 4.0 簡介
  本主題提供 DiffGram 的簡介。  
  
## <a name="diffgram-format"></a>DiffGram 格式  
 這是一般 DiffGram 格式：  
  
```  
<?xml version="1.0"?>  
<diffgr:diffgram   
         xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"  
         xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1"  
         xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
   <DataInstance>  
      ...  
   </DataInstance>  
   [<diffgr:before>  
        ...  
   </diffgr:before>]  
  
   [<diffgr:errors>  
        ...  
   </diffgr:errors>]  
</diffgr:diffgram>  
```  
  
 DiffGram 格式由下列區塊組成：  
  
 **\<DataInstance>**  
 此元素的名稱**DataInstance**是用於本檔中的說明。 例如，如果從 .NET Framework 中的資料集產生 DiffGram，則會使用資料集的**name**屬性值做為此元素的名稱。 這個區塊包含變更之後的所有相關資料，可能包括尚未修改的資料。 DiffGram 處理邏輯會忽略此區塊中未指定**diffgr： hasChanges**屬性的元素。  
  
 **\<diffgr：之前>**  
 這個選擇性區塊包含必須更新或刪除的原始記錄執行個體 (元素)。 DiffGram 所修改（更新或刪除）的所有資料庫資料表，都必須在 [ ** \< before>** ] 區塊中顯示為最上層的元素。  
  
 **\<diffgr：錯誤>**  
 DiffGram 處理邏輯會忽略這個選擇性區塊。  
  
## <a name="diffgram-annotations"></a>DiffGram 註解  
 這些注釋定義于 DiffGram 命名空間 **"urn：架構-microsoft-com： xml-DiffGram-01"** 中：  
  
 **id**  
 這個屬性是用來配對中的元素， ** \<>** 和** \< DataInstance>** 組塊。  
  
 **hasChanges**  
 若為插入或更新作業，DiffGram 必須使用已**插入**或**已修改**的值來指定此屬性。 如果這個屬性不存在，處理邏輯會忽略** \< DataInstance>** 中的對應元素，而且不會執行任何更新。 如需工作範例，請參閱[&#40;SQLXML 4.0&#41;的 DiffGram 範例](diffgram-examples-sqlxml-4-0.md)。  
  
 **parentID**  
 這個屬性是用來在 DiffGram 的元素之間指定父子式關聯性。 這個屬性只會出現在 [ \< before>] 區塊中。 SQLXML 會在套用更新時使用此屬性。 此父子式關聯性會用於決定處理 DiffGram 中元素的順序。  
  
## <a name="understanding-the-diffgram-processing-logic"></a>了解 DiffGram 處理邏輯  
 DiffGram 處理邏輯會使用特定規則來判斷某項作業是插入、更新或刪除作業。 下表將描述這些規則。  
  
|作業|描述|  
|---------------|-----------------|  
|插入|當專案出現在** \< DataInstance>** 區塊中，而不是在對應的** \<>** 區塊中，而且在專案上指定了**Diffgr： hasChanges**屬性（**diffgr： hasChanges =**）時，DiffGram 就表示插入作業。 在此情況下，DiffGram 會將** \< DataInstance>** 區塊中指定的記錄實例插入資料庫中。<br /><br /> 如果未指定**diffgr： hasChanges**屬性，處理邏輯會忽略元素，而且不會執行任何插入。 如需工作範例，請參閱[&#40;SQLXML 4.0&#41;的 DiffGram 範例](diffgram-examples-sqlxml-4-0.md)。|  
|更新|DiffGram 表示在 [before>] 區塊中有一個專案時，如果 \< ** \< DataInstance>** 區塊中有一個對應的元素（也就是說，這兩個專案都有一個具有相同值的**diffgr： id**屬性），而且**diffgr： hasChanges**屬性是以** \< DataInstance>** 區塊中專案上**修改**的值所指定，則為更新作業。<br /><br /> 如果** \< DataInstance>** 區塊的元素上未指定**diffgr： hasChanges**屬性，處理邏輯會傳回錯誤。 如需工作範例，請參閱[&#40;SQLXML 4.0&#41;的 DiffGram 範例](diffgram-examples-sqlxml-4-0.md)。<br /><br /> 如果在** \<>區塊之前**指定了**Diffgr： parentid** ， **parentid**所指定之元素的父子式關聯性會用於判斷記錄的更新順序。|  
|刪除|當元素出現在** \< before>** 區塊中，但不在對應的** \< DataInstance>** 區塊中時，DiffGram 表示刪除作業。 在此情況下，DiffGram 會從資料庫刪除** \< before>** 區塊中指定的記錄實例。 如需工作範例，請參閱[&#40;SQLXML 4.0&#41;的 DiffGram 範例](diffgram-examples-sqlxml-4-0.md)。<br /><br /> 如果在** \<>區塊之前**指定了**Diffgr： parentid** ， **parentid**所指定之元素的父子式關聯性會用於判斷記錄的刪除順序。|  
  
> [!NOTE]  
>  參數無法傳遞給 DiffGram。  
  
  
