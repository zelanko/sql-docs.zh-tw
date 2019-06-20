---
title: 編輯類型對應 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 184f7ab2-725f-491e-a15b-b889f2fb6a68
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 98b7c0433e506d7ef6e825199a9a6629c52e6f3b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63183088"
---
# <a name="edit-type-mapping-mysqltosql"></a>編輯類型對應 (MySQLToSQL)
**編輯類型對應**對話方塊可讓您指定類型的來源和目的地的資料庫物件之間的對應方式。  
  
您可以存取此對話方塊中，在幾個地方：  
  
-   當您選取來源資料庫或資料庫物件**型別對應**右邊的 [中繼資料總管] 會出現的索引標籤。 按一下 [**新增**以加入新的型別對應，或按一下**編輯**若要變更現有的型別對應。  
  
-   在 [**工具**功能表上，選取**專案設定**或是**預設專案設定**。 在出現的對話方塊中，選取**型別對應**。 按一下 [**新增**以加入新的型別對應，或按一下**編輯**若要變更現有的型別對應。  
  
-   資料表特定的型別對應會覆寫資料庫，以及專案型別對應。 特定資料庫的對應會覆寫專案對應。  
  
## <a name="options"></a>選項  
  
##### <a name="source-type"></a>來源類型  
選取來源資料類型對應至 SQL Server 資料型別。  
  
下列欄位的可變長度資料類型時，會出現下**Sourcetype**:  
  
##### <a name="from"></a>來源  
指定此對應的最小長度。 例如，對於**nchar**資料類型，您可以輸入 10，以指定此對應是範圍開始**nchar(10)。**  
  
##### <a name="to"></a>若要  
指定此對應的最大長度。 例如，對於**nchar**資料類型，您可以輸入以指定此對應是範圍結束時間的 20 **nchar(20)。**  
  
##### <a name="target-type"></a>目標類型  
選取來源資料類型會對應至 SQL Server 資料類型。 SSMA 會將資料表建立時或在 SQL Server 中，來源資料類型會變成此資料型別。  
  
下列欄位的可變長度資料類型時，會出現下**目標類型**:  
  
##### <a name="replace-with"></a>取代成  
指定此對應的目標長度。 例如，對於**nvarchar**資料類型，您可以輸入來指定指定的來源資料類型都應該對應至 20 **nvarchar (20)。**  
  
