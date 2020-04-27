---
title: 定義屬性關聯性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [Analysis Services], relationships
- relationships [Analysis Services], attributes
ms.assetid: 9184d344-e96d-4025-ad6f-3f75129746df
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 47a46bfd482463de2377470cd11186bd3bfbd5db
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66077055"
---
# <a name="define-attribute-relationships"></a>定義屬性關聯性
  在[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，屬性是維度的基礎建立區塊。 維度包含一組根據屬性關聯性所組織的屬性。  
  
 針對包含在維度中的每個資料表，有一種屬性關聯性可以建立資料表之重要屬性與該資料表中之其他屬性的關聯性。 建立維度時，您可以建立這種關聯性。  
  
 屬性關聯性提供下列優點：  
  
-   減少維度處理所需的記憶體量。 這會加快維度、磁碟分割和查詢的處理速度。  
  
-   由於儲存體存取速度更快，而且執行計劃的最佳化程度更好，因此可以增加查詢效能。  
  
-   假設已沿著關聯性路徑定義使用者自訂階層，則按照彙總設計演算法選取彙總時更有效率。  
  
    > [!NOTE]  
    >  如需定義和設定屬性關聯性之重要性和含意的詳細資訊，請參閱《 [SQL Server 2005 Analysis Services 效能指南》](https://docsbay.net/Microsoft-SQL-Server-2005-Analysis-Services-Performance-Guide)中的「加強查詢效能」一節。  
  
## <a name="attribute-relationship-considerations"></a>屬性關聯性考量  
 當基礎資料支援屬性關聯性時，您也應該定義屬性之間的唯一屬性關聯性。 若要定義唯一屬性關聯性，使用 [維度設計師] 的 [屬性關聯性]**** 索引標籤。  
  
 具有輸出關聯性的屬性必須具備相對於其相關聯屬性的唯一索引鍵。 換句話說，來源屬性中的成員在相關聯的屬性中，必須識別一個 (而且只能識別一個) 成員。 例如，請考量 City -> State 的關聯性。 在此關聯性中，來源屬性為 [City]，而相關聯的屬性為 [State]。 Source 屬性是「多」端，而相關端是多對一關聯性的「一」端。 來源屬性的索引鍵將是 City + State。 如需詳細資訊，請參閱 [建立、修改或刪除屬性關聯性](attribute-relationships-create-modify-or-delete-relationship.md)。  
  
 如需屬性 (Attribute) 關聯性之屬性 (Property) 的詳細資訊，請參閱 [設定屬性 (Attribute) 關聯性屬性 (Property)](attribute-relationships-configure-attribute-properties.md)。  
  
> [!NOTE]  
>  如果定義的屬性關聯性錯誤，可能導致查詢結果無效。  
  
## <a name="see-also"></a>另請參閱  
 [屬性關聯性](../multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)  
  
  
