---
title: 將 Access 資料庫移轉至 SQL Server-Azure SQL DB |Microsoft 文件
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 08/15/2017
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
- instructions, migration
- migrating databases, overview
- overview, migration process
- procedure, migration
- recommended migration process
ms.assetid: 76a3abcf-2998-4712-9490-fe8d872c89ca
caps.latest.revision: 23
author: Shamikg
ms.author: Shamikg
manager: murato
ms.workload: On Demand
ms.openlocfilehash: bbbea4be309e1508620e9e067c94328905fcc824
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="migrating-access-databases-to-sql-server---azure-sql-db-accesstosql"></a>將 Access 資料庫移轉至 SQL Server-Azure SQL DB (AccessToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 移轉小幫手 (SSMA) 是一種工具，提供完整的環境，可協助您快速存取資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 您可以藉由使用 SSMA，檢閱存取和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 資料庫物件、 評估 Access 資料庫移轉，將存取資料庫物件、 載入到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，然後再移轉資料。  
  
## <a name="recommended-migration-process"></a>建議的移轉程序  
若要成功移轉物件和資料，從存取[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，請使用下列程序：  
  
1.  [建立新的 SSMA 專案](http://msdn.microsoft.com/f2d1f0b0-5394-4adb-b3f3-abd71eb68ca7)。 建立專案之後，您可以[設定專案選項](http://msdn.microsoft.com/0a7304df-2f35-4453-96ef-7ac83dea1167)，包括轉換選項、 移轉選項，以及資料類型對應。  
  
2.  [加入 Access 資料庫檔案](http://msdn.microsoft.com/e944c740-4c8a-4bc1-b0ed-be57bc06dced)至專案。  
  
    您可以加入個別的檔案，包括電腦或網路上的找到檔案。  
  
3.  [連接到目標 SQL Server 執行個體](http://msdn.microsoft.com/f84cf007-ddf1-4396-a07c-3e0729abc769)或[連接到 SQL Azure 的目標執行個體](http://msdn.microsoft.com/1ba0d113-dc05-4431-8689-e14a8821bafd)。  
  
    您可以連接到 SQL Server 或 SQL Azure。  
  
4.  若要自訂一個或多個 Access 資料庫之間的對應和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 的結構描述，[對應來源和目標資料庫](http://msdn.microsoft.com/69bee937-7b2c-49ee-8866-7518c683fad4)。  
  
5.  您可以選擇性地[建立評估報表](http://msdn.microsoft.com/8b9e23d6-da62-437a-8c05-8ad2628b9441)來判斷是否存取資料庫物件可以成功地轉換成[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。  
  
6.  [將存取資料庫物件](http://msdn.microsoft.com/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 物件定義。  
  
7.  [轉換的資料庫物件載入 SQL Server](http://msdn.microsoft.com/4e854eee-b10c-4f0b-9d9e-d92416e6f2ba)。  
  
    您可以載入到其中一個資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 使用 SSMA，或者您可以儲存[!INCLUDE[tsql](../../includes/tsql_md.md)]指令碼。  
  
8.  [將存取資料移轉至 SQL Server](http://msdn.microsoft.com/f3b18af7-1af0-499d-a00d-a0af94895625)。  
  
    > [!NOTE]  
    > 您可以將轉換、 載入及移轉結構描述和一個步驟中的資料。 若要執行一種單鍵移轉，請按一下**轉換、 載入和移轉** 按鈕。  
  
9. 如果您想要使用的資料在應用程式存取[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，使用[Access 資料表連結至 SQL Server 資料表](http://msdn.microsoft.com/82374ad2-7737-4164-a489-13261ba393d4)。  
  
您也可以使用 「 移轉精靈 」，引導您完成此程序。 如需詳細資訊，請參閱[移轉精靈](http://msdn.microsoft.com/5bab5914-b2ae-4795-8cf5-83e42d64bef2)。  
  
## <a name="see-also"></a>另請參閱  
[開始使用 SQL Server 移轉小幫手進行存取](http://msdn.microsoft.com/462a731f-08f1-44e1-9eeb-4deac6d2f6c5)  
[準備移轉的 Access 資料庫](http://msdn.microsoft.com/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)
