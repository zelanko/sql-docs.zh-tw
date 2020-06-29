---
title: 建立資料表的 SQL 陳述式 (SQL Server 匯入和匯出精靈) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.createtablesql.f1
ms.assetid: 0d6f6b3b-d023-4770-a8a9-65b2977c8d05
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d3fc2054711708a27691f2d7219c33749f11b977
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85424955"
---
# <a name="create-table-sql-statement-sql-server-import-and-export-wizard"></a>建立資料表的 SQL 陳述式 (SQL Server 匯入和匯出精靈)
  使用 [**建立資料表的 SQL 語句**] 對話方塊，即可查看自動產生的語句，或針對您的用途加以修改。 如果您修改此陳述式，就可能也必須對資料行對應進行相關的變更，而且此後必須手動維護已編輯的 SQL 陳述式。  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會根據連接的資料來源來產生預設 CREATE TABLE 陳述式。 這個預設 CREATE TABLE 陳述式將不會包含 FILESTREAM 屬性，即使來源資料表包含有宣告 FILESTREAM 屬性的資料行亦然。 若要執行具有 FILESTREAM 屬性的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 元件，請先在目的地資料庫上實作 FILESTREAM 儲存體。 然後在 **[建立資料表]** 對話方塊中，將 FILESTREAM 屬性加入至 CREATE TABLE 陳述式。 如需詳細資訊，請參閱[二進位大型物件 &#40;Blob&#41; 資料 &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)。  
  
 若要深入瞭解此嚮導，請參閱[SQL Server 匯入和匯出嚮導](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要瞭解用來啟動精靈的選項，以及成功執行嚮導所需的許可權，請參閱[執行 SQL Server 匯入和匯出嚮導](start-the-sql-server-import-and-export-wizard.md)。  
  
 「SQL Server 匯入和匯出精靈」的用途在於將資料從來源複製到目的地。 這個精靈也可以為您建立目的地資料庫和目的地資料表。 不過，如果您必須複製多個資料庫或資料表，或複製其他種類的資料庫物件，則應該改用「複製資料庫精靈」。 如需詳細資訊，請參閱 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="options"></a>選項  
 **SQL 語句**  
 顯示自動產生的 SQL 陳述式並進行編輯。  
  
> [!NOTE]  
>  如果要在 SQL 陳述式中包含歸位字元，請按 CTRL+ENTER 鍵。 如果只按 ENTER 鍵，對話方塊就會關閉。  
  
 **自動產生**  
 按一下 [自動產生]****，還原預設的 SQL 陳述式 (如果已修改的話)。  
  
  
