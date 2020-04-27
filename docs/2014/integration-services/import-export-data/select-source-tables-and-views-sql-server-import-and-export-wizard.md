---
title: 選取來源資料表和檢視 (SQL Server 匯入和匯出精靈) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.selectsourcetablesandviews.f1
ms.assetid: f60e1a19-2ea6-403c-89ab-3e60ac533ea0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 479cc0e650c598e0a253caca796b854dc4eb69cd
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62892666"
---
# <a name="select-source-tables-and-views-sql-server-import-and-export-wizard"></a>選取來源資料表和檢視 (SQL Server 匯入和匯出精靈)
  使用 [**選取來源資料表和資料檢視**] 頁面，即可指定要從資料來源複製到目的地的資料表和 views。  
  
> [!NOTE]  
>  當您選取 [資料表複製] 選項時，並不必複製資料表中的所有資料行。 選取目的地資料表之後，請按一下 [編輯對應] 以顯示 [資料**行**對應] 對話方塊。 針對您要略過的資料行，在 [資料**行**對應] 對話方塊的 [**目的地**] 資料行中，選取** \<[忽略>** ]。  
  
 若要深入瞭解此嚮導，請參閱[SQL Server 匯入和匯出嚮導](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要瞭解啟動精靈的選項，以及成功執行嚮導所需的許可權，請參閱[執行 SQL Server 匯入和匯出嚮導](start-the-sql-server-import-and-export-wizard.md)。  
  
 「SQL Server 匯入和匯出精靈」的用途在於將資料從來源複製到目的地。 這個精靈也可以為您建立目的地資料庫和目的地資料表。 不過，如果您必須複製多個資料庫或資料表，或複製其他種類的資料庫物件，則應該改用「複製資料庫精靈」。 如需詳細資訊，請參閱 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="options"></a>選項。  
  
### <a name="tables-and-views-list"></a>資料表和檢視表清單  
 **來源**  
 使用這些核取方塊，從可用的資料表和檢視清單中選取要複製到目的地的項目。 如果您選取來源資料表或檢視，並且未執行其他任何動作，就會複製來自來源的結構描述和資料，而不會進行變更。  
  
 **Destination**  
 從每個來源資料表的清單中選取目的地資料表。  
  
> [!NOTE]  
>  如果此時在精靈中暫停，使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或其他工具在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中建立目的地資料表，並不能立刻在可用的目的地資料表清單中看到新的資料表。 若要重新整理目的地資料表清單，請將兩個頁面移至 [**選擇目的地**] 頁面上，再次選取目的地資料庫，然後再次前進到 [**選取來源資料表和資料檢視]**。  
  
### <a name="other-options"></a>其他選項  
 **編輯對應**  
 使用 [資料**行**對應] 對話方塊，即可指定要接收來源資料的目的地資料行。 您可以針對想要略過的資料行\<，在 [資料**行**對應] 對話方塊的 [**目的地**] 資料行中，選取 [忽略>]，只複製資料行的子集。  
  
 **預覽**  
 在執行匯入或匯出之前，預覽 [**預覽資料**] 對話方塊中的來源資料以進行驗證。 [**預覽資料**] 對話方塊會顯示多達200個數據列。  
  
 預覽資料之後，您可能會想要變更已針對資料來源和目的地選取的選項。 若要進行這些變更，請在 [選取來源資料表和檢視]**** 頁面上，按 [上一步]**** 返回先前的頁面，如此您就可以在其中變更選項。  
  
  
