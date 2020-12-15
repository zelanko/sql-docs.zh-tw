---
title: DiffGrams 的 SQLXML 4.0 簡介
description: 瞭解 SQLXML 4.0 中 Diffgram 的格式、注釋和處理邏輯。
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotations [SQLXML]
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: 1902d67f-baf3-46e6-a36c-b24b5ba6f8ea
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 66a58dfb19cf8f53f775bac663d5ba3e6147711b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97414940"
---
# <a name="introduction-to-diffgrams-in-sqlxml-40"></a>DiffGrams 的 SQLXML 4.0 簡介
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
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
 此元素的名稱 **DataInstance**，用於本檔中的說明用途。 例如，如果 DiffGram 是從 .NET Framework 中的資料集產生的，則會使用資料集的 **name** 屬性值做為此元素的名稱。 這個區塊包含變更之後的所有相關資料，可能包括尚未修改的資料。 DiffGram 處理邏輯會忽略這個區塊中未指定 **diffgr： hasChanges** 屬性的元素。  
  
 **\<diffgr:before>**  
 這個選擇性區塊包含必須更新或刪除的原始記錄執行個體 (元素)。 自 DiffGram)  (更新或刪除的所有資料庫資料表，都必須顯示為區塊中的最上層元素 **\<before>** 。  
  
 **\<diffgr:errors>**  
 DiffGram 處理邏輯會忽略這個選擇性區塊。  
  
## <a name="diffgram-annotations"></a>DiffGram 註解  
 這些注釋定義于 DiffGram 命名空間 **"urn：架構-microsoft-com： xml-DiffGram-01"**：  
  
 **id**  
 這個屬性是用來配對和區塊中的元素 **\<before>** **\<DataInstance>** 。  
  
 **hasChanges**  
 針對插入或更新作業，DiffGram 必須使用 **插入** 或 **修改** 的值來指定此屬性。 如果這個屬性不存在，處理邏輯會忽略中的對應元素， **\<DataInstance>** 而且不會執行任何更新。 如需實用的範例，請參閱 [&#40;SQLXML 4.0&#41;的 DiffGram 範例 ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md)。  
  
 **parentID**  
 這個屬性是用來在 DiffGram 的元素之間指定父子式關聯性。 這個屬性只會出現在 \<before> 區塊中。 SQLXML 會在套用更新時使用此屬性。 此父子式關聯性會用於決定處理 DiffGram 中元素的順序。  
  
## <a name="understanding-the-diffgram-processing-logic"></a>了解 DiffGram 處理邏輯  
 DiffGram 處理邏輯會使用特定規則來判斷某項作業是插入、更新或刪除作業。 下表將描述這些規則。  
  
|作業|描述|  
|---------------|-----------------|  
|插入|當元素出現在 **\<DataInstance>** 區塊中，而不是在對應的 **\<before>** 區塊中，而且已指定 **diffgr： hasChanges** 屬性 (**diffgr： hasChanges =** 在元素上插入) 時，DiffGram 會指出插入作業。 在此情況下，DiffGram 會將區塊中指定的記錄實例插入 **\<DataInstance>** 至資料庫。<br /><br /> 如果未指定 **diffgr： hasChanges** 屬性，處理邏輯會忽略元素，而且不會執行任何插入。 如需實用的範例，請參閱 [&#40;SQLXML 4.0&#41;的 DiffGram 範例 ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md)。|  
|更新|如果區塊中有一個專案在區塊中有一個對應的元素，則 DiffGram 表示一個更新作業 \<before> **\<DataInstance>** (也就是說，這兩個專案都有一個具有相同值的 **diffgr： id** 屬性) ，而 **diffgr： hasChanges** 屬性則是使用在區塊的元素上 **修改** 的值來指定 **\<DataInstance>** 。<br /><br /> 如果區塊中的元素未指定 **diffgr： hasChanges** 屬性 **\<DataInstance>** ，處理邏輯會傳回錯誤。 如需實用的範例，請參閱 [&#40;SQLXML 4.0&#41;的 DiffGram 範例 ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md)。<br /><br /> 如果在區塊中指定 **diffgr： parentid** ，則會 **\<before>** 使用 **parentid** 所指定之元素的父子式關聯性來決定更新記錄的順序。|  
|刪除|DiffGram 指出當元素出現在區塊中， **\<before>** 而不是在對應的區塊中時的刪除作業 **\<DataInstance>** 。 在此情況下，DiffGram 會從資料庫中刪除區塊中指定的記錄實例 **\<before>** 。 如需實用的範例，請參閱 [&#40;SQLXML 4.0&#41;的 DiffGram 範例 ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md)。<br /><br /> 如果在區塊中指定 **diffgr： parentid** ，則會 **\<before>** 使用 **parentid** 所指定之元素的父子式關聯性來決定刪除記錄的順序。|  
  
> [!NOTE]  
>  參數無法傳遞給 DiffGram。  
  
  
