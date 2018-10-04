---
title: 選取來源資料表和檢視 (SQL Server 匯入和匯出精靈) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.selectsourcetablesandviews.f1
ms.assetid: f60e1a19-2ea6-403c-89ab-3e60ac533ea0
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2f99b94c133ba2a8bfd8bbe6d7b78bd455061409
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48050130"
---
# <a name="select-source-tables-and-views-sql-server-import-and-export-wizard"></a>選取來源資料表和檢視 (SQL Server 匯入和匯出精靈)
  使用**選取來源資料表和檢視**頁面以指定的資料表和檢視，以從資料來源複製到目的地。  
  
> [!NOTE]  
>  當您選取 [資料表複製] 選項時，並不必複製資料表中的所有資料行。 選取目的地資料表之後, 按一下 編輯對應，顯示**資料行對應** 對話方塊。 選取  **\<忽略 >** 中**目的地**資料行**資料行對應**對話方塊中，針對您想要跳過的資料行。  
  
 若要深入了解此精靈，請參閱[SQL Server 匯入和匯出精靈](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要深入了解啟動精靈，選項和相關的權限，才能成功執行精靈，請參閱[執行 SQL Server 匯入和匯出精靈](start-the-sql-server-import-and-export-wizard.md)。  
  
 「SQL Server 匯入和匯出精靈」的用途在於將資料從來源複製到目的地。 這個精靈也可以為您建立目的地資料庫和目的地資料表。 不過，如果您必須複製多個資料庫或資料表，或複製其他種類的資料庫物件，則應該改用「複製資料庫精靈」。 如需詳細資訊，請參閱 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="options"></a>選項。  
  
### <a name="tables-and-views-list"></a>資料表和檢視表清單  
 **Source**  
 使用這些核取方塊，從可用的資料表和檢視清單中選取要複製到目的地的項目。 如果您選取來源資料表或檢視，並且未執行其他任何動作，就會複製來自來源的結構描述和資料，而不會進行變更。  
  
 **目的地**  
 從每個來源資料表的清單中選取目的地資料表。  
  
> [!NOTE]  
>  如果您暫停在此精靈來建立目的地資料表的這一點[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]或另一個工具，新的資料表沒有立即顯示在清單中可用的目的地資料表。 若要重新整理目的地資料表清單，請退後兩頁要**選擇目的地**頁面上，重新選取目的地資料庫，然後再次前進到**選取來源資料表和檢視**。  
  
### <a name="other-options"></a>其他選項  
 **編輯對應**  
 使用**資料行對應**對話方塊來指定要接收來源資料的目的地資料行。 您可以透過選取複製的資料行子集\<忽略 > 中**目的地**資料行**資料行對應**對話方塊中，針對您想要跳過的資料行。  
  
 **預覽**  
 預覽中的來源資料**預覽資料**對話方塊中，確認之前執行匯入或匯出。 **預覽資料**對話方塊會顯示最多 200 個資料列。  
  
 預覽資料之後，您可能會想要變更已針對資料來源和目的地選取的選項。 若要進行這些變更，請在 [選取來源資料表和檢視] 頁面上，按 [上一步] 返回先前的頁面，如此您就可以在其中變更選項。  
  
  
