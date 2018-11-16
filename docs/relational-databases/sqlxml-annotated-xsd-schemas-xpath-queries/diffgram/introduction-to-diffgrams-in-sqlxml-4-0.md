---
title: SQLXML 4.0 的 Diffgram 簡介 |Microsoft Docs
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
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 567c4b6054623fad160dc17378e2a4a680fc4c8e
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51669507"
---
# <a name="introduction-to-diffgrams-in-sqlxml-40"></a>DiffGrams 的 SQLXML 4.0 簡介
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  本主題提供 DiffGram 的簡介。  
  
## <a name="diffgram-format"></a>DiffGram 格式  
 這是一般 DiffGram 格式：  
  
```  
<?xml version="1.0"?>  
<diffgr:diffgram   
         xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"  
         xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1"  
         xmlns:xsd="https://www.w3.org/2001/XMLSchema">  
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
  
 **\<DataInstance >**  
 這個元素的名稱**DataInstance**，用於說明用途，此文件中。 例如，如果從.NET Framework 中，windows 7 中的資料集所產生的 DiffGram**名稱**資料集屬性做為這個項目的名稱。 這個區塊包含變更之後的所有相關資料，可能包括尚未修改的資料。 DiffGram 處理邏輯會忽略此區塊中的項目， **diffgr: haschanges**未指定屬性。  
  
 **\<diffgr:before>**  
 這個選擇性區塊包含必須更新或刪除的原始記錄執行個體 (元素)。 正在修改 （更新或刪除） 的所有資料庫都資料表 diffgram 必須顯示為最上層項目的**\<之前 >** 區塊。  
  
 **\<diffgr:errors>**  
 DiffGram 處理邏輯會忽略這個選擇性區塊。  
  
## <a name="diffgram-annotations"></a>DiffGram 註解  
 DiffGram 命名空間中定義這些附註 **"urn: schemas-microsoft-microsoft-schemas-microsoft-com:-diffgram-01"**:  
  
 **id**  
 此屬性用來在項目進行配對**\<之前 >** 並 **\<DataInstance >** 區塊。  
  
 **hasChanges**  
 插入或更新作業，DiffGram 必須指定此屬性具有值**插入**或是**修改**。 如果這個屬性不存在中的對應項目 **\<DataInstance >** 忽略處理邏輯，而且沒有更新會執行。 如需實用範例，請參閱[DiffGram 範例&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md)。  
  
 **parentID**  
 這個屬性是用來在 DiffGram 的元素之間指定父子式關聯性。 這個屬性只會顯示在\<之前 > 區塊。 SQLXML 會在套用更新時使用此屬性。 此父子式關聯性會用於決定處理 DiffGram 中元素的順序。  
  
## <a name="understanding-the-diffgram-processing-logic"></a>了解 DiffGram 處理邏輯  
 DiffGram 處理邏輯會使用特定規則來判斷某項作業是插入、更新或刪除作業。 下表將描述這些規則。  
  
|作業|描述|  
|---------------|-----------------|  
|Insert|中的項目出現時，DiffGram 就代表插入作業 **\<DataInstance >** 區塊但不是在對應**\<之前 >** 區塊，以及**diffgr: haschanges**指定屬性 (**diffgr: haschanges = 插入**) 項目上。 在此情況下，DiffGram 插入記錄執行個體中指定 **\<DataInstance >** 區塊至資料庫。<br /><br /> 如果**diffgr: haschanges**未指定屬性、 項目會被忽略，處理邏輯，會執行任何插入。 如需實用範例，請參閱[DiffGram 範例&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md)。|  
|Update|中的項目時，DiffGram 就代表更新作業\<之前 > 區塊中的對應項目是 **\<DataInstance >** 區塊 （也就是這兩個元素具有**diffgr: id**具有相同值的屬性) 和**diffgr: haschanges**屬性會指定值**修改**中的項目上**\<DataInstance >** 區塊。<br /><br /> 如果**diffgr: haschanges**中的項目未指定屬性，則 **\<DataInstance >** 區塊，則會傳回錯誤，處理邏輯。 如需實用範例，請參閱[DiffGram 範例&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md)。<br /><br /> 如果**diffgr: parentid**中指定**\<之前 >** 區塊中，項目所指定的父子式關聯性**parentID**中使用決定更新記錄的順序。|  
|DELETE|中的項目出現時，DiffGram 就代表刪除作業**\<之前 >** 區塊但不是在對應 **\<DataInstance >** 區塊。 在此情況下，DiffGram 刪除記錄執行個體中指定**\<之前 >** 從資料庫的區塊。 如需實用範例，請參閱[DiffGram 範例&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md)。<br /><br /> 如果**diffgr: parentid**中指定**\<之前 >** 區塊中，項目所指定的父子式關聯性**parentID**中使用決定刪除記錄的順序。|  
  
> [!NOTE]  
>  參數無法傳遞給 DiffGram。  
  
  
