---
title: 將 Access 資料移轉到 SQL Server-Azure SQL DB (AccessToSQL) |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67907138"
---
# <a name="migrating-access-data-into-sql-server---azure-sql-db-accesstosql"></a>將 Access 資料移轉到 SQL Server-Azure SQL DB (AccessToSQL)
您已成功建立資料庫物件之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您可以將資料從存取移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。  
  
## <a name="setting-migration-options"></a>移轉選項的設定  
在移轉資料之前先[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，檢閱中的專案移轉選項**專案設定** 對話方塊。 在此對話方塊中，您可以設定移轉的批次大小、 資料表鎖定、 條件約束檢查，插入觸發程序引發時，身分識別與 null 值處理，以及如何處理日期，而超出[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]範圍。 如需詳細資訊，請參閱 <<c0> [ 專案設定 （移轉）](https://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d)。  
  
## <a name="migrating-data"></a>將資料移轉  
移轉資料時，它會將資料插入的資料列大量載入作業[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或在交易中的 SQL Azure。 要載入的資料列數目[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或專案設定中設定 SQL Azure 中的每個交易。  
  
若要檢視移轉訊息，請確定 [輸出] 窗格會顯示。 如果未列出，請在**檢視**功能表上，選取**輸出**。  
  
**若要將資料移轉**  
  
1.  請確定您已載入至 Access 資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。  
  
2.  在存取中繼資料總管 中，選取包含您想要移轉之資料的物件：  
  
    -   若要將整個資料庫的資料移轉，選取資料庫名稱旁邊的核取方塊。  
  
    -   若要從個別的資料表移轉資料，展開資料庫，再展開**資料表**，然後選取 資料表旁的核取方塊。 若要省略來自個別資料表的資料，清除核取方塊。  
  
3.  以滑鼠右鍵按一下**資料庫**，然後選取**移轉資料**。  
  
您也可以使用將資料移轉之外 SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **bcp**命令列公用程式或[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。 如需有關這些工具的詳細資訊，請參閱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]線上叢書 》。  
  
## <a name="next-step"></a>下一個步驟  
如果您有想要繼續使用在移轉之後存取資料庫應用程式時，連結至 Access 資料庫資料表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 資料表。 如需詳細資訊，請參閱 <<c0> [ 連結至 SQL Server 的 Access 應用程式](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)。  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[設定轉換和移轉選項](setting-conversion-and-migration-options-accesstosql.md)  
  
