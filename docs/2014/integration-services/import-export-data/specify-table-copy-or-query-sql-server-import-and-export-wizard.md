---
title: 指定資料表複製或查詢 (SQL Server 匯入和匯出精靈) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.specifytablecopyorquery.f1
ms.assetid: 08aa7158-40e6-4ef3-84d3-1265a8ba194c
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 51f195a9f5fbe97eadfc281ad50bd0de55d6151e
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965528"
---
# <a name="specify-table-copy-or-query-sql-server-import-and-export-wizard"></a>指定資料表複製或查詢 (SQL Server 匯入和匯出精靈)
  使用 [**指定資料表複製或查詢**] 頁面，即可指定如何複製資料。 您可以使用圖形介面來選取要複製的現有資料庫物件，或使用 Transact-SQL 來建立更複雜的查詢。  
  
 若要深入瞭解此嚮導，請參閱[SQL Server 匯入和匯出嚮導](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要瞭解用來啟動精靈的選項，以及成功執行嚮導所需的許可權，請參閱[執行 SQL Server 匯入和匯出嚮導](start-the-sql-server-import-and-export-wizard.md)。  
  
 「SQL Server 匯入和匯出精靈」的用途在於將資料從來源複製到目的地。 這個精靈也可以為您建立目的地資料庫和目的地資料表。 不過，如果您必須複製多個資料庫或資料表，或複製其他種類的資料庫物件，則應該改用「複製資料庫精靈」。 如需詳細資訊，請參閱 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="options"></a>選項。  
 **從一或多個資料表或視圖複製資料**  
 使用 [**選取來源資料表和流覽**器] 對話方塊，將欄位從選取的來源資料表和視圖複製到指定的目的地或目的地。 如果您要複製來源的所有資料，但不要篩選或排序記錄，請使用此選項。  
  
 當您使用 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者來連接至資料來源時，可能會無法使用 **[從一或多個資料表或檢視表複製資料]** 選項。 這個選項僅適用於在 ProviderDescriptors.xml 檔案中具有 ProviderDescription 區段的提供者。 每個 ProviderDescription 區段會包含從對應提供者擷取中繼資料所需的資訊。 根據預設，只有下列提供者的 ProviderDescriptors.xml 檔案包含 ProviderDescription 區段：  
  
-   System.Data.SqlClient  
  
-   System.Data.OracleClient  
  
-   System.Data.OleDb  
  
-   System.Data.Odbc  
  
 若要讓其他提供者可以使用 [**從一個或多個資料表或視圖來複製資料]** 選項，協力廠商可將自己的 ProviderDescriptor 區段新增至 ProviderDescriptors.xml 檔案。 根據預設，此檔案位於 \<*drive*> ： \Program FILES\MICROSOFT SQL server\100\dts\providerdescriptors。 若要檢閱 ProviderDescriptor 區段的需求，請參閱 ProviderDescriptors.xsd 結構描述檔案 (預設與 ProviderDescriptors.xml 檔案位於相同的資料夾中)。  
  
 **撰寫查詢來指定要傳送的資料**  
 使用 [**提供來源查詢**] 對話方塊來建立 SQL 語句，以取得資料列。 如果您要在進行複製作業時修改或限制來源資料，請使用此選項。 只有符合選取準則的資料列可供複製。  
  
  
