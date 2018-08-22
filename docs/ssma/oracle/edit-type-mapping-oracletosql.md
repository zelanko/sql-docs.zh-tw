---
title: 編輯類型對應 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 7078b4ed-c779-4bf3-8db8-f9dcb3edd50f
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: c9225773588810e4843525e271faa7023d9ce172
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2018
ms.locfileid: "40393146"
---
# <a name="edit-type-mapping-oracletosql"></a>編輯類型對應 (OracleToSQL)
**編輯類型對應**對話方塊可讓您指定類型的來源和目的地的資料庫物件之間的對應方式。  
  
您可以存取此對話方塊中，在幾個地方：  
  
-   當您選取來源資料庫或資料庫物件**型別對應**右邊的 [中繼資料總管] 會出現的索引標籤。 按一下 **新增**以加入新的型別對應，或按一下**編輯**若要變更現有的型別對應。  
  
-   在 **工具**功能表上，選取**專案設定**或是**預設專案設定**。 在出現的對話方塊中，選取**型別對應**。 按一下 **新增**以加入新的型別對應，或按一下**編輯**若要變更現有的型別對應。  
  
資料表特定的型別對應會覆寫資料庫，以及專案型別對應。 特定資料庫的對應會覆寫專案對應。  
  
## <a name="options"></a>選項。  
**來源類型**  
選取來源資料類型對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料型別。  
  
下列欄位的可變長度資料類型時，會出現下**來源類型**:  
  
**來源**  
指定此對應的最小長度。 例如，對於**nchar**資料類型，您可以輸入 10，以指定此對應是範圍開始**nchar(10)**。  
  
**若要**  
指定此對應的最大長度。 例如，對於**nchar**資料類型，您可以輸入以指定此對應是範圍結束時間的 20 **nchar(20)**。  
  
**目標類型**  
選取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所對應至來源資料類型的資料類型。 SSMA 當建立資料表或預存程序[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，來源資料類型會變更為此資料型別。  
  
下列欄位的可變長度資料類型時，會出現下**目標類型**:  
  
**Replace with**  
指定此對應的目標長度。 例如，對於**nvarchar**資料類型，您可以輸入來指定指定的來源資料類型都應該對應至 20 **nvarchar(20)**。  
  
