---
title: 將 Access 資料庫移轉至 SQL Server-Azure SQL DB |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- instructions, migration
- migrating databases, overview
- overview, migration process
- procedure, migration
- recommended migration process
ms.assetid: 76a3abcf-2998-4712-9490-fe8d872c89ca
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: b15ecd732acf373dbc5cee817983305c1d792fe4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47683706"
---
# <a name="migrating-access-databases-to-sql-server---azure-sql-db-accesstosql"></a>Access 資料庫移轉到 SQL Server-Azure SQL DB (AccessToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 移轉小幫手 (SSMA) 是一種工具，提供完整的環境，可協助您快速存取資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 使用 SSMA，您可以檢閱存取權並[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 資料庫物件、 評定移轉的 Access 資料庫、 將 Access 資料庫物件的轉換、 載入到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，然後移轉資料。  
  
## <a name="recommended-migration-process"></a>建議的移轉程序  
若要成功移轉物件和資料，從存取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，使用下列程序：  
  
1.  [建立新的 SSMA 專案](creating-and-managing-projects-accesstosql.md)。 建立專案之後，您可以[設定專案選項](setting-conversion-and-migration-options-accesstosql.md)，包括轉換選項、 移轉選項，以及資料類型對應。  
  
2.  [加入 Access 資料庫檔案](adding-and-removing-access-database-files-accesstosql.md)至專案。  
  
    您可以新增個別的檔案，包含電腦或網路上的找到檔案。  
  
3.  [連接到 SQL Server 目標執行個體](connecting-to-sql-server-accesstosql.md)或是[連接到 SQL Azure 的目標執行個體](connecting-to-azure-sql-db-accesstosql.md)。  
  
    您可以連接到 SQL Server 或 SQL Azure。  
  
4.  若要自訂一個或多個 Access 資料庫之間的對應並[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 的結構描述[對應來源和目標資料庫](mapping-source-and-target-databases-accesstosql.md)。  
  
5.  您可以選擇[建立評量報告](assessing-access-database-objects-for-conversion-accesstosql.md)來判斷是否存取資料庫物件可以成功轉換成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。  
  
6.  [轉換 Access 資料庫物件](converting-access-database-objects-accesstosql.md)至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 物件定義。  
  
7.  [已轉換的資料庫物件載入 SQL Server](loading-converted-database-objects-into-sql-server-accesstosql.md)。  
  
    您可以載入至任一個資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 使用 SSMA，或者您可以儲存[!INCLUDE[tsql](../../includes/tsql-md.md)]指令碼。  
  
8.  [將 Access 資料移轉至 SQL Server](migrating-access-data-into-sql-server-azure-sql-db-accesstosql.md)。  
  
    > [!NOTE]  
    > 您可以將轉換、 載入及移轉結構描述和一個步驟中的資料。 若要執行一種單鍵移轉，請按一下**轉換、 載入和移轉** 按鈕。  
  
9. 如果您想要存取應用程式以使用中的資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，使用[的 Access 資料表連結到 SQL Server 資料表](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)。  
  
您也可以使用 「 移轉精靈 」，引導您完成此程序。 如需詳細資訊，請參閱 <<c0> [ 遷移精靈](migration-wizard-accesstosql.md)。  
  
## <a name="see-also"></a>另請參閱  
[Getting Started with SQL Server 移轉小幫手，存取](getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)  
[準備移轉的 Access 資料庫](preparing-access-databases-for-migration-accesstosql.md)
