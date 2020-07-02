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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 749623542b7611498f1a3014d733bd086cb75900
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85650036"
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
 此元素的名稱**DataInstance**是用於本檔中的說明。 例如，如果從 .NET Framework 中的資料集產生 DiffGram，則會使用資料集的**name**屬性值做為此元素的名稱。 這個區塊包含變更之後的所有相關資料，可能包括尚未修改的資料。 DiffGram 處理邏輯會忽略此區塊中未指定**diffgr： hasChanges**屬性的元素。  
  
 **\<diffgr:before>**  
 這個選擇性區塊包含必須更新或刪除的原始記錄執行個體 (元素)。 DiffGram 所修改（更新或刪除）的所有資料庫資料表，都必須在區塊中顯示為最上層元素 **\<before>** 。  
  
 **\<diffgr:errors>**  
 DiffGram 處理邏輯會忽略這個選擇性區塊。  
  
## <a name="diffgram-annotations"></a>DiffGram 註解  
 這些注釋定義于 DiffGram 命名空間 **"urn：架構-microsoft-com： xml-DiffGram-01"** 中：  
  
 **id**  
 這個屬性是用來配對和區塊中的元素 **\<before>** **\<DataInstance>** 。  
  
 **hasChanges**  
 若為插入或更新作業，DiffGram 必須使用已**插入**或**已修改**的值來指定此屬性。 如果這個屬性不存在，處理邏輯會忽略中的對應元素， **\<DataInstance>** 而且不會執行任何更新。 如需工作範例，請參閱[&#40;SQLXML 4.0&#41;的 DiffGram 範例](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md)。  
  
 **parentID**  
 這個屬性是用來在 DiffGram 的元素之間指定父子式關聯性。 這個屬性只會出現在 \<before> 區塊中。 SQLXML 會在套用更新時使用此屬性。 此父子式關聯性會用於決定處理 DiffGram 中元素的順序。  
  
## <a name="understanding-the-diffgram-processing-logic"></a>了解 DiffGram 處理邏輯  
 DiffGram 處理邏輯會使用特定規則來判斷某項作業是插入、更新或刪除作業。 下表將描述這些規則。  
  
|作業|描述|  
|---------------|-----------------|  
|插入|當元素出現在 **\<DataInstance>** 區塊中，而不是在對應的 **\<before>** 區塊中，而且在專案上指定了**diffgr： hasChanges**屬性（**diffgr： HasChanges =**）時，DiffGram 就代表插入作業。 在此情況下，DiffGram 會將區塊中指定的記錄實例插入 **\<DataInstance>** 資料庫中。<br /><br /> 如果未指定**diffgr： hasChanges**屬性，處理邏輯會忽略元素，而且不會執行任何插入。 如需工作範例，請參閱[&#40;SQLXML 4.0&#41;的 DiffGram 範例](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md)。|  
|更新|當區塊中有一個對應專案的元素時，DiffGram 會指出更新作業 \<before> **\<DataInstance>** （也就是說，這兩個專案都具有具有相同值的**diffgr： id**屬性），而且**diffgr： hasChanges**屬性是以在區塊中的專案上**修改**的值所指定 **\<DataInstance>** 。<br /><br /> 如果未在區塊的元素上指定**diffgr： hasChanges**屬性 **\<DataInstance>** ，處理邏輯就會傳回錯誤。 如需工作範例，請參閱[&#40;SQLXML 4.0&#41;的 DiffGram 範例](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md)。<br /><br /> 如果在區塊中指定**diffgr： parentid** **\<before>** ， **parentid**所指定之元素的父子式關聯性會用於判斷記錄的更新順序。|  
|刪除|當元素出現在區塊中， **\<before>** 而不是在對應的區塊中時，DiffGram 表示刪除作業 **\<DataInstance>** 。 在此情況下，DiffGram 會從資料庫中刪除在區塊中指定的記錄實例 **\<before>** 。 如需工作範例，請參閱[&#40;SQLXML 4.0&#41;的 DiffGram 範例](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md)。<br /><br /> 如果在區塊中指定**diffgr： parentid** **\<before>** ， **parentid**所指定之元素的父子式關聯性會用於判斷刪除記錄的順序。|  
  
> [!NOTE]  
>  參數無法傳遞給 DiffGram。  
  
  
