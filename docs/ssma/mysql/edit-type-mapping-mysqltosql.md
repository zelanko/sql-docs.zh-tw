---
title: "編輯類型對應 (MySQLToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-mysql
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 184f7ab2-725f-491e-a15b-b889f2fb6a68
caps.latest.revision: "4"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8db4278a82968a5bd147f5fcb984af3fa104022e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="edit-type-mapping-mysqltosql"></a>編輯類型對應 (MySQLToSQL)
**編輯類型對應** 對話方塊可讓您指定來源和目的地的資料庫物件之間如何對應型別。  
  
您可以存取此對話方塊，在幾個地方：  
  
-   當您選取來源資料庫或資料庫物件**類型對應**右邊的 [中繼資料總管] 索引標籤會出現。 按一下**新增**加入新的型別對應，或按一下**編輯**若要變更現有的型別對應。  
  
-   在**工具**功能表上，選取**專案設定**或**預設專案設定**。 在 [結果] 對話方塊中，選取**類型對應**。 按一下**新增**加入新的型別對應，或按一下**編輯**若要變更現有的型別對應。  
  
-   特定資料表的型別對應會覆寫資料庫，和專案類型對應。 特定資料庫的對應覆寫專案對應。  
  
## <a name="options"></a>選項。  
  
##### <a name="source-type"></a>來源類型  
選取來源資料類型對應至 SQL Server 資料型別。  
  
如果資料類型是可變長度，下列欄位會出現在**Sourcetype**:  
  
##### <a name="from"></a>來源  
指定針對此對應的最小長度。 例如，對於**nchar**資料類型，您可以輸入 10，以指定此對應是範圍開始**nchar(10)。**  
  
##### <a name="to"></a>若要  
指定此對應的最大長度。 例如，對於**nchar**資料類型，您可以輸入 20 來指定此對應的結束時間範圍**nchar(20)。**  
  
##### <a name="target-type"></a>目標類型  
選取來源資料類型對應到 SQL Server 資料類型。 SSMA 會將資料表建立時或在 SQL Server 中，來源資料類型會變更為此資料類型。  
  
如果資料類型是可變長度，下列欄位會出現在**目標類型**:  
  
##### <a name="replace-with"></a>取代成  
指定針對此對應的目標長度。 例如，對於**nvarchar**資料類型，您可以輸入 20 指定指定之來源資料類型應該對應至**nvarchar (20)。**  
  
