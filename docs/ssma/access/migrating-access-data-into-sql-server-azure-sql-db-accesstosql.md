---
title: 將存取資料移轉到 SQL Server-Azure SQL DB (AccessToSQL) |Microsoft 文件
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
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
caps.latest.revision: 17
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 937d75eb150a65bf65d1f55c01c5de760f0d36d4
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2018
---
# <a name="migrating-access-data-into-sql-server---azure-sql-db-accesstosql"></a>將存取資料移轉到 SQL Server-Azure SQL DB (AccessToSQL)
您已成功建立資料庫物件之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，您可以移轉資料的存取權從[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。  
  
## <a name="setting-migration-options"></a>移轉選項的設定  
移轉資料之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 中，檢閱中的專案移轉選項**專案設定** 對話方塊。 在此對話方塊，您可以設定移轉的批次大小、 鎖定資料表、 條件約束檢查，插入觸發程序引發時，身分識別與 null 值處理，以及如何處理日期，而不[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]範圍。 如需詳細資訊，請參閱[（移轉） 的專案設定](http://msdn.microsoft.com/en-us/4caebc9c-8680-4b99-a8fa-89c43161c95d)。  
  
## <a name="migrating-data"></a>將資料移轉  
移轉資料會移到資料列大量載入作業[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 中的交易。 要載入的資料列數目[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或專案設定中設定 SQL Azure 中的每個交易。  
  
若要檢視移轉的訊息，請確定輸出窗格已顯示。 如果未列出，請在**檢視**功能表上，選取**輸出**。  
  
**若要將資料移轉**  
  
1.  請確定您已載入到存取資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。  
  
2.  在存取中繼資料總管，選取包含您想要移轉之資料的物件：  
  
    -   若要將整個資料庫的資料移轉，選取資料庫名稱旁邊的核取方塊。  
  
    -   若要從個別的資料表移轉資料，依序展開資料庫、**資料表**，然後選取資料表旁的核取方塊。 若要省略來自個別資料表的資料，請清除核取方塊。  
  
3.  以滑鼠右鍵按一下**資料庫**，然後選取 **移轉資料**。  
  
您也可以移轉資料之外 SSMA 使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **bcp**命令列公用程式或[!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)]。 如需有關這些工具的詳細資訊，請參閱[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]線上叢書 》。  
  
## <a name="next-step"></a>下一個步驟  
如果您有存取您想要繼續移轉之後使用的資料庫應用程式時，連結至 Access 資料庫資料表[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 的資料表。 如需詳細資訊，請參閱[連結到 SQL Server 存取應用程式](http://msdn.microsoft.com/en-us/82374ad2-7737-4164-a489-13261ba393d4)。  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
[設定轉換和移轉選項](http://msdn.microsoft.com/en-us/0a7304df-2f35-4453-96ef-7ac83dea1167)  
  
