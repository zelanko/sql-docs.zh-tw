---
title: 指定資料表複製或查詢 (SQL Server 匯入和匯出精靈) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.impexpwizard.specifytablecopyorquery.f1
ms.assetid: 08aa7158-40e6-4ef3-84d3-1265a8ba194c
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 413dd857be0ab913f43bd07f9c2f82d536137dad
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034818"
---
# <a name="specify-table-copy-or-query-sql-server-import-and-export-wizard"></a>指定資料表複製或查詢 (SQL Server 匯入和匯出精靈)
  使用**指定資料表複製或查詢**頁面，即可指定如何複製資料。 您可以使用圖形介面來選取要複製的現有資料庫物件，或使用 Transact-SQL 來建立更複雜的查詢。  
  
 若要深入了解這個精靈，請參閱[SQL Server 匯入和匯出精靈](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要深入了解啟動精靈，以及成功執行精靈所需的權限的選項，請參閱[執行 SQL Server 匯入和匯出精靈](start-the-sql-server-import-and-export-wizard.md)。  
  
 「SQL Server 匯入和匯出精靈」的用途在於將資料從來源複製到目的地。 這個精靈也可以為您建立目的地資料庫和目的地資料表。 不過，如果您必須複製多個資料庫或資料表，或複製其他種類的資料庫物件，則應該改用「複製資料庫精靈」。 如需詳細資訊，請參閱 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="options"></a>選項。  
 **從一個或多個資料表或檢視表複製資料**  
 將欄位從選取的來源資料表和檢視表複製到指定的目的地，使用**選取來源資料表和檢視** 對話方塊。 如果您要複製來源的所有資料，但不要篩選或排序記錄，請使用此選項。  
  
 當您使用[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]資料提供者連接至資料來源時，**從一或多個資料表或檢視表複製資料**選項可能無法使用。 這個選項僅適用於在 ProviderDescriptors.xml 檔案中具有 ProviderDescription 區段的提供者。 每個 ProviderDescription 區段會包含從對應提供者擷取中繼資料所需的資訊。 根據預設，只有下列提供者的 ProviderDescriptors.xml 檔案包含 ProviderDescription 區段：  
  
-   System.Data.SqlClient  
  
-   System.Data.OracleClient  
  
-   System.Data.OleDb  
  
-   System.Data.Odbc  
  
 若要讓**從一或多個資料表或檢視表複製資料**選項可供其他提供者、 協力廠商可以將自己的 ProviderDescriptor 區段加入至 ProviderDescriptors.xml 檔案。 根據預設，這個檔案位於\<*磁碟機*>: \Program Files\Microsoft SQL Server\100\DTS\ProviderDescriptors。 若要檢閱 ProviderDescriptor 區段的需求，請參閱 ProviderDescriptors.xsd 結構描述檔案 (預設與 ProviderDescriptors.xml 檔案位於相同的資料夾中)。  
  
 **撰寫查詢來指定要傳送的資料**  
 建立 SQL 陳述式來擷取資料列使用**提供來源查詢** 對話方塊。 如果您要在進行複製作業時修改或限制來源資料，請使用此選項。 只有符合選取準則的資料列可供複製。  
  
  