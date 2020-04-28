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
ms.openlocfilehash: 959af9bcb1879dc19d2bfb99253b4c40d637fd1e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68260238"
---
# <a name="migrating-access-databases-to-sql-server---azure-sql-db-accesstosql"></a>將 Access 資料庫移轉至 SQL Server-Azure SQL DB （AccessToSQL）
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]移轉小幫手（SSMA）是一種工具，可提供全方位的環境，協助您快速將 Access [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫移轉至或 SQL Azure。 藉由使用 SSMA，您可以查看存取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和或 SQL Azure 資料庫物件、評估 access 資料庫的遷移、轉換 access 資料庫物件、將其載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，然後再遷移資料。  
  
## <a name="recommended-migration-process"></a>建議的移轉程序  
若要成功地將物件和資料從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]存取權遷移到或 SQL Azure，請使用下列程式：  
  
1.  [建立新的 SSMA 專案](creating-and-managing-projects-accesstosql.md)。 建立專案之後，您可以[設定專案選項](setting-conversion-and-migration-options-accesstosql.md)，包括轉換選項、遷移選項和資料類型對應。  
  
2.  [將 Access 資料庫檔案加入](adding-and-removing-access-database-files-accesstosql.md)至專案。  
  
    您可以新增個別檔案，包括您在電腦或網路上找到的檔案。  
  
3.  [連接到 SQL Server 的目標實例](connecting-to-sql-server-accesstosql.md)，或[連接到 SQL Azure 的目標實例](connecting-to-azure-sql-db-accesstosql.md)。  
  
    您可以連接到 SQL Server 或 SQL Azure。  
  
4.  若要自訂一或多個 Access 資料庫和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 架構之間的對應，請[對應來源和目標資料庫](mapping-source-and-target-databases-accesstosql.md)。  
  
5.  （選擇性）您可以[建立評估報告](assessing-access-database-objects-for-conversion-accesstosql.md)，以判斷 Access 資料庫物件是否可以成功轉換為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。  
  
6.  [將 Access 資料庫物件轉換](converting-access-database-objects-accesstosql.md)成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 物件定義。  
  
7.  [將轉換的資料庫物件載入 SQL Server](loading-converted-database-objects-into-sql-server-accesstosql.md)。  
  
    您可以使用 SSMA，將資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]載入或 SQL Azure，或者可以儲存[!INCLUDE[tsql](../../includes/tsql-md.md)]腳本。  
  
8.  將[存取資料移轉到 SQL Server](migrating-access-data-into-sql-server-azure-sql-db-accesstosql.md)。  
  
    > [!NOTE]  
    > 您可以在一個步驟中轉換、載入和遷移架構和資料。 若要執行單鍵遷移，請按一下 [**轉換]、[載入] 和 [遷移**] 按鈕。  
  
9. 如果您想要讓 Access 應用程式使用或 SQL [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Azure 中的資料，請使用 [將[存取資料表連結到 SQL Server 資料表]](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)。  
  
您也可以使用 [遷移嚮導] 引導您完成此程式。 如需詳細資訊，請參閱[遷移 Wizard](migration-wizard-accesstosql.md)。  
  
## <a name="see-also"></a>另請參閱  
[具有存取權 SQL Server 移轉小幫手的消費者入門](getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)  
[準備 Access 資料庫以進行遷移](preparing-access-databases-for-migration-accesstosql.md)
