---
title: 定義資料庫維度 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- dimensions [Analysis Services], defining
ms.assetid: fe84588b-66a3-4100-a1cf-59b21b7adf01
caps.latest.revision: 26
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c71a335db4b17f365bcb40ebf4c7cefb13c30b3c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37269904"
---
# <a name="define-database-dimensions"></a>定義資料庫維度
  使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的維度設計師來設定 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案或資料庫中的現有資料庫維度。 您可以使用 [維度設計師] 執行下列動作：  
  
-   設定維度層級屬性 (Property)。  
  
-   加入及設定維度屬性 (Attribute)。  
  
-   定義及設定使用者自訂階層。  
  
-   定義及設定屬性 (Attribute) 之間關聯性。  
  
-   定義維度翻譯。  
  
-   如果是已處理的維度，您可以瀏覽此維度結構及檢視資料。  
  
 修改維度、屬性或階層之後，必須處理該維度，才能檢視變更。 在專案模式下工作時，要在處理之前部署變更至 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體。  
  
 如需如何在維度設計師中開啟維度的詳細資訊，請參閱 [在方案總管中修改或刪除資料庫維度](database-dimensions-modify-or-delete-a-database-dimension-in-solution-explorer.md)。  
  
 維度設計師有三個不同的索引標籤，下表就是這些索引標籤的描述。  
  
|索引標籤|描述|  
|---------|-----------------|  
|**維度結構**|使用此索引標籤搭配維度的結構使用 - 檢查或建立維度的資料來源檢視結構描述、使用屬性，以及組織使用者自訂階層中的屬性。|  
|**中，使用 [維度設計師] 的**|使用這個索引標籤，即可建立、修改或刪除維度的屬性關聯性。|  
|**翻譯**|使用此索引標籤，以不同語言加入及編輯維度中繼資料的翻譯。|  
|**瀏覽器**|使用此索引標籤，檢查已處理維度的成員，以及檢閱維度中繼資料的翻譯。|  
  
 下列主題描述可以在 [維度設計師] 中執行的工作。  
  
 [維度屬性內容參考](dimension-attribute-properties-reference.md)  
 描述如何定義及設定維度屬性。  
  
 [建立使用者定義階層](user-defined-hierarchies-create.md)  
 描述如何定義及設定使用者自訂階層。  
  
 [定義屬性關聯性](attribute-relationships-define.md)  
 描述如何定義及設定屬性關聯性。  
  
 [使用商業智慧精靈增強維度](../use-the-business-intelligence-wizard-to-enhance-dimensions.md)  
 描述如何使用「商業智慧精靈」來增強維度。  
  
  
