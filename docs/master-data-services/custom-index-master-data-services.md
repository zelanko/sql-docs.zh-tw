---
title: 自訂索引 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
ms.assetid: c57bf8b8-55a6-4b6c-9adb-91b5f4f1ee3c
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 5d52335f4b80a4cd1ff06e9fe8084d46a8d0d089
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47854996"
---
# <a name="custom-index-master-data-services"></a>自訂索引 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  自訂索引會在實體中於單一屬性 (單一索引) 或一份屬性清單 (複合索引) 上建立非叢集索引。 索引一般會改善查詢程序的效能。 如需 SQL Server 索引的詳細資訊，請參閱 [索引](../relational-databases/indexes/indexes.md)。  
  
## <a name="type-of-indexes"></a>索引類型  
 您可以針對每個實體建立下列類型的多個自訂索引。  
  
-   唯一索引  
  
-   非唯一索引  
  
 唯一索引確保索引資料行未包含重複值。 針對複合唯一索引，此索引確保所選取屬性清單的每一個值組合都是唯一的。 如果所選取屬性的值重複，則無法建立唯一索引。  
  
## <a name="rules"></a>規則  
 下列規則適用於自訂的唯一和非唯一索引。  
  
-   若要建立自訂索引，請確定您選取至少一個屬性。  
  
-   如果您嘗試儲存具有相同屬性清單和唯一性旗標作為另一個索引的索引，則無法儲存索引。 會顯示錯誤。  
  
    > [!NOTE]  
    >  MDS 會自動建立特定屬性的索引 (例如 DBA 和程式碼)。 這表示您無法建立另一個索引，這個索引包含其中一個屬性但未包含任何其他屬性。  
  
-   只要其他索引中至少有一個不同的屬性，屬性就可以包含在多個自訂索引中。 否則，索引都會相同。  
  
-   如果您建立的索引包含多個屬性或大型大小的屬性，而且所選屬性的總大小超過索引鍵大小上限 (900 個位元組)，則無法儲存索引。  
  
-   自訂索引可以建立於分葉成員屬性 (檔案屬性除外) 上。  
  
-   如果您想要刪除自訂索引中所含的屬性，則適用下列項目。  
  
    -   如果只在一個屬性上建立索引 (單一索引)，則會同時刪除屬性和索引。  
  
    -   如果在多個屬性上建立索引 (複合索引)，則無法在編輯索引之前刪除屬性。  
  
-   無法變更自訂索引中所含的屬性類型。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|建立索引|[建立索引 &#40;Master Data Services&#41;](../master-data-services/create-an-index-master-data-services.md)|  
|編輯和刪除索引|[編輯和刪除索引 &#40;Master Data Services&#41;](../master-data-services/edit-and-delete-an-index-master-data-services.md)|  
  
  
