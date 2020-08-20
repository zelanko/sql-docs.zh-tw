---
description: '將存取資料移轉至 SQL Server Azure SQL Database (AccessToSQL) '
title: 將存取資料移轉至 SQL Server Azure SQL Database (AccessToSQL) |Microsoft Docs
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
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: c44f7af6972c316322d4a81b7de9fa13b77205a0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488291"
---
# <a name="migrating-access-data-into-sql-server---azure-sql-database-accesstosql"></a>將存取資料移轉至 SQL Server Azure SQL Database (AccessToSQL) 
當您成功建立資料庫物件至之後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，您可以將資料從存取權遷移至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure。  
  
## <a name="setting-migration-options"></a>設定遷移選項  
在您將資料移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 之前，請先在 [ **專案設定** ] 對話方塊中，檢查項目遷移選項。 在這個對話方塊中，您可以設定遷移批次大小、表鎖、條件約束檢查、插入觸發程式引發、身分識別和 null 值處理，以及如何處理超出範圍的日期 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如需詳細資訊，請參閱 [ (遷移) 的專案設定 ](https://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d)。  
  
## <a name="migrating-data"></a>遷移資料  
遷移資料是一項大量載入作業，可將資料列移入或移至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Azure 中的交易。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]每一筆交易中要載入或 SQL Azure 的資料列數，都是在專案設定中設定。  
  
若要查看遷移訊息，請確認 [輸出] 窗格是可見的。 如果不是，請在 [ **視圖** ] 功能表上選取 [ **輸出**]。  
  
**遷移資料**  
  
1.  請確定您已將 Access 資料庫物件載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure。  
  
2.  在 [存取中繼資料瀏覽器] 中，選取包含您想要遷移之資料的物件：  
  
    -   若要遷移整個資料庫的資料，請選取資料庫名稱旁邊的核取方塊。  
  
    -   若要從個別資料表遷移資料，請展開資料庫，展開 [ **資料表**]，然後選取資料表旁的核取方塊。 若要省略個別資料表中的資料，請清除此核取方塊。  
  
3.  以滑鼠右鍵按一下 [ **資料庫** ]，然後選取 [ **遷移資料**]。  
  
您也可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **bcp** 命令列公用程式或，在 SSMA 外部遷移資料 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 。 如需這些工具的詳細資訊，請參閱《 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》。  
  
## <a name="next-step"></a>後續步驟  
如果您有想要在遷移後繼續使用的資料庫應用程式，請將 Access 資料庫資料表連結至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 資料表。 如需詳細資訊，請參閱 [將 Access 應用程式連結至 SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)。  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[設定轉換和遷移選項](setting-conversion-and-migration-options-accesstosql.md)  
  
