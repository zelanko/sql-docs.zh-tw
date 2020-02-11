---
title: 將存取資料移轉至 SQL Server-Azure SQL DB （AccessToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- bulk loading data
- data, loading into SQL Azure
- data, loading into SQL Server
- migrating databases, loading data
- migrating databases, options
- options, migrating data
- SQL Azure, migrating data into
- SQL Server, migrating data into
ms.assetid: f3b18af7-1af0-499d-a00d-a0af94895625
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 8f0e93efee0c57c904c32ec52fbb560f973f21b8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67907138"
---
# <a name="migrating-access-data-into-sql-server---azure-sql-db-accesstosql"></a>將存取資料移轉至 SQL Server-Azure SQL DB （AccessToSQL）
成功建立資料庫物件之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您可以將資料從存取權遷移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。  
  
## <a name="setting-migration-options"></a>設定遷移選項  
將資料移轉到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 之前，請先參閱 [**專案設定**] 對話方塊中的專案遷移選項。 在此對話方塊中，您可以設定「遷移批次大小」、「資料表鎖定」、「條件約束檢查」、「插入觸發程式引發」、「識別」和「null [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]值」處理，以及如何處理超出範圍的日期。 如需詳細資訊，請參閱[專案設定（遷移）](https://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d)。  
  
## <a name="migrating-data"></a>遷移資料  
遷移資料是大量載入作業，會在交易中將資料列[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]移入或 SQL Azure。 要在每個交易中載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 的資料列數目，會在專案設定中設定。  
  
若要查看遷移訊息，請確定 [輸出] 窗格是可見的。 如果不是，請在 [ **View** ] 功能表上選取 [**輸出**]。  
  
**遷移資料**  
  
1.  請確定您已將 Access 資料庫物件載入或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Azure 中。  
  
2.  在 [存取中繼資料 Explorer] 中，選取包含您想要遷移之資料的物件：  
  
    -   若要遷移整個資料庫的資料，請選取資料庫名稱旁邊的核取方塊。  
  
    -   若要從個別資料表遷移資料，請展開資料庫，展開 [**資料表**]，然後選取資料表旁的核取方塊。 若要省略個別資料表中的資料，請清除此核取方塊。  
  
3.  以滑鼠右鍵按一下 [**資料庫**]，然後選取 [**遷移資料**]。  
  
您也可以使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **bcp**命令列公用程式或[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]，在 SSMA 外部遷移資料。 如需這些工具的詳細資訊， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]請參閱《線上叢書》。  
  
## <a name="next-step"></a>後續步驟  
如果您有在遷移之後想要繼續使用的資料庫應用程式，請將 Access 資料庫資料表連結到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 資料表。 如需詳細資訊，請參閱[將存取應用程式連結至 SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)。  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[設定轉換和遷移選項](setting-conversion-and-migration-options-accesstosql.md)  
  
