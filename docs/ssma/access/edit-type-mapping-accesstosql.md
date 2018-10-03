---
title: 編輯類型對應 (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 7f9d9530-6c04-41d9-bbe7-d91820a30066
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 2bbe1636db483ad24f7744fe4d9902c520e07dbb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47675406"
---
# <a name="edit-type-mapping-accesstosql"></a>編輯類型對應 (AccessToSQL)
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
指定此對應的最小長度。 例如，對於**文字**資料類型，您可以輸入 10，以指定此對應是範圍開始**text(10)**。  
  
**若要**  
指定此對應的最大長度。 例如，對於**文字**資料類型，您可以輸入以指定此對應是範圍結束時間的 20 **text(20)**。  
  
**目標類型**  
選取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所對應至來源資料類型的資料類型。 SSMA 當建立資料表或預存程序[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，來源資料類型會變更為此資料型別。  
  
下列欄位的可變長度資料類型時，會出現下**目標類型**:  
  
**Replace with**  
指定此對應的目標長度。 例如，對於**nvarchar**資料類型，您可以輸入來指定指定的來源資料類型都應該對應至 20 **nvarchar(20)**。  
  
