---
title: 名稱比對 （資料來源檢視精靈） (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.datasourceviewwizard.namematchingcriteria.f1
ms.assetid: 7f811e02-0fe6-45c9-a7b7-29c61032d96b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 866bdea710033a0cfa3bdadb34282c96c810d730
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66072399"
---
# <a name="name-matching-data-source-view-wizard-analysis-services"></a>名稱比對 (資料來源檢視精靈) (Analysis Services)
  使用 **[名稱比對]** 頁面並選取要使用的準則，即可偵測您為資料來源檢視所選取的資料表，與結構描述中的其他資料表是否有關聯性。 如果兩個資料表之間不存在實體外部索引鍵的關聯性，此準則可以幫助您識別相關的資料表，並將資料表加入資料來源檢視。 由名稱比對識別的邏輯關聯性，也會加入到資料來源檢視中。  
  
> [!NOTE]  
>  只有當您選取的資料來源有多個資料表，但各個資料表間沒有任何外部索引鍵關聯性時，才會顯示這個頁面。  
  
## <a name="options"></a>選項。  
 **比對資料行來建立邏輯關聯性**  
 選取即可使用名稱比對準則，來偵測您選取要包含在資料來源檢視中的資料表，與結構描述中的其他資料表是否有邏輯相依性和關聯性。 如果您清除此核取方塊，就不會在資料來源中使用名稱比對準則來識別資料表之間的邏輯關聯性。  
  
 **外部索引鍵的相符項目**  
 選取建立資料表之間的邏輯關聯性和資料來源中的檢視所使用的準則。 比對字串中的非英數字元會被忽略。 例如，「Customer ID」、「Customer_ID」和「CustomerID」全部都會相符。 選取下表的選項之一，即可以指定的條件建立關聯性。  
  
|Select|即可建立|  
|------------|---------------|  
|**與主索引鍵的名稱相同**|資料行名稱符合所選資料表之主索引鍵資料行名稱的任何資料表之邏輯關聯性。|  
|**與目的地資料表的名稱相同**|資料行名稱符合所選資料表名稱的任何資料表之邏輯關聯性。|  
|**目的地資料表名稱 + 主索引鍵名稱**|資料行名稱符合所選資料表名稱串連所選資料表之主索引鍵資料行名稱的邏輯關聯性。 串連字串中的非英數字元會被忽略 (例如，「Product ID」、「Product_ID」和「ProductID」全部都會相符)。|  
  
 **描述及範例**  
 檢視所選準則的描述及範例。  
  
  
