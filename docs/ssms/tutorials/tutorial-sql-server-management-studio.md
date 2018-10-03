---
title: 教學課程：SQL Server Management Studio (SSMS) | Microsoft Docs
ms.custom: ''
ms.date: 08/30/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.tutorialstart.ssms.f1
helpviewer_keywords:
- projects [SQL Server Management Studio], tutorials
- templates [SQL Server], SQL Server Management Studio
- source controls [SQL Server Management Studio], tutorials
- Help [SQL Server], SQL Server Management Studio
- tutorials [SQL Server Management Studio]
- Transact-SQL tutorials
- solutions [SQL Server Management Studio], tutorials
- SQL Server Management Studio [SQL Server], tutorials
- scripts [SQL Server], SQL Server Management Studio
ms.assetid: d2bade70-07cf-4d94-b5d2-88aecb538ed1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9d262e2d2a4c79a44f0b5a5245991f32b3676487
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47723866"
---
# <a name="tutorials-for-sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS) 教學課程
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

SQL Server Management Studio (SSMS) 教學課程將為您介紹用來管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 基礎結構的整合式環境。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供設定、監視和管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的圖形介面。 也讓您部署、監視以及升級應用程式所使用的資料層元件，例如資料庫。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 也提供用於編輯和偵錯指令碼的 [!INCLUDE[tsql](../../includes/tsql-md.md)]、MDX、DMX 和 XML 語言編輯器。  
  
## <a name="what-you-will-learn"></a>學習內容  

本系列教學課程將協助您了解資訊在 SSMS 中的呈現方式，以及如何運用其功能。
  
熟悉 SSMS 的最佳方式是實際練習。 本系列教學課程將讓您熟悉 SSMS 中可用的各項功能。  本系列教學課程會告訴您如何管理 SSMS 的元件及如何尋找您經常使用的功能。  

以下是這些教學課程所涵蓋的內容： 

  
- [教學課程：使用 SSMS 對 SQL Server 進行連線與查詢](connect-query-sql-server.md)

    在本教學課程中，您將學習如何連線至您的 SQL Server 執行個體。 您也將學習一些基本的 Transact-SQL (T-SQL) 命令來建立和查詢新的資料庫。 

- [教學課程：在 SSMS 中撰寫物件指令碼](scripting-ssms.md)

    在本教學課程中，您將學習如何在 SSMS 中編寫各種物件的指令碼，包括資料庫和查詢。 

- [教學課程：在 SSMS 中使用範本](templates-ssms.md)
   
    在本教學課程中，您將學習如何使用在 SSMS 中預先建立的範本。 範本是鮮為人知的功能，其中存放了各種資料庫系統管理工作的大量 Transact-SQL 程式碼片段。 

- [教學課程： SSMS 設定](ssms-configuration.md)

    在本教學課程中，您將學習設定 SSMS 環境的基礎，例如變更環境配置。 本教學課程也會說明各種不同的 SSMS 元件。 
  

- [教學課程：使用 SSMS 的其他祕訣與訣竅](ssms-tricks.md)

    在本教學課程中，您將學習使用 SSMS 的其他秘訣與訣竅。 本教學課程包含下列項目：
    - 註解、取消註解文字
    - 縮排文字
    - 在物件總管中篩選物件
    - 存取您的 SQL Server 錯誤記錄檔
    - 尋找您的執行個體名稱 
 
  
## <a name="requirements"></a>需求  
這個教學課程適合不熟悉 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]，但很熟悉資料庫概念和 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的資深資料庫管理員和資料庫開發人員。  
  
您必須已經安裝下列項目，才能使用這個教學課程：  

  -   下載最新版的 [SQL Server Management Studio (SSMS)](../download-sql-server-management-studio-ssms.md)。  

第一節將引導您建立資料庫，但也可以在此處找到其他範例資料庫：[AdventureWorks Sample Databases](https://github.com/Microsoft/sql-server-samples/releases) (AdventureWorks 範例資料庫)。 此處可以找到在 SSMS 中還原資料庫的說明：[還原資料庫](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)。 


  
## <a name="see-also"></a>另請參閱  
[Database Engine 教學課程](../../relational-databases/database-engine-tutorials.md)          
  
  
  

