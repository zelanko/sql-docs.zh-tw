---
title: "編輯類型對應 (DB2ToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: f93c4b7d-74fc-4856-bf42-035289918e83
caps.latest.revision: "4"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 92bc671abed684b7653a44229f5732d71ac7f271
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="edit-type-mapping-db2tosql"></a>編輯類型對應 (DB2ToSQL)
**編輯類型對應** 對話方塊可讓您指定來源和目的地的資料庫物件之間如何對應型別。  
  
您可以存取此對話方塊，在幾個地方：  
  
-   當您選取來源資料庫或資料庫物件**類型對應**右邊的 [中繼資料總管] 索引標籤會出現。 按一下**新增**加入新的型別對應，或按一下**編輯**若要變更現有的型別對應。  
  
-   在**工具**功能表上，選取**專案設定**或**預設專案設定**。 在 [結果] 對話方塊中，選取**類型對應**。 按一下**新增**加入新的型別對應，或按一下**編輯**若要變更現有的型別對應。  
  
特定資料表的型別對應會覆寫資料庫，和專案類型對應。 特定資料庫的對應覆寫專案對應。  
  
## <a name="options"></a>選項。  
**來源類型**  
選取來源資料類型對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料型別。  
  
如果資料類型是可變長度，下列欄位會出現在**來源類型**:  
  
**來源**  
指定針對此對應的最小長度。 例如，對於**nchar**資料類型，您可以輸入 10，以指定此對應是範圍開始**nchar(10)**。  
  
**若要**  
指定此對應的最大長度。 例如，對於**nchar**資料類型，您可以輸入 20 來指定此對應的結束時間範圍**nchar(20)**。  
  
**目標類型**  
選取[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]來源資料類型對應的資料類型。 SSMA 當建立資料表或預存程序中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，來源資料類型會變更為此資料類型。  
  
如果資料類型是可變長度，下列欄位會出現在**目標類型**:  
  
**Replace with**  
指定針對此對應的目標長度。 例如，對於**nvarchar**資料類型，您可以輸入 20 指定指定之來源資料類型應該對應至**nvarchar （20)**。  
  
