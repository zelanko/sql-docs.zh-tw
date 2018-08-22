---
title: 存取 (AccessToSQL) 的 SQL Server 移轉小幫手 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/14/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 40c1eb02-26b2-44ba-969d-6c430c61c281
caps.latest.revision: 22
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: 6ba577e5b8ec0ea365487bef1ee8ac786efd8459
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2018
ms.locfileid: "40396262"
---
# <a name="sql-server-migration-assistant-for-access-accesstosql"></a>存取 (AccessToSQL) 的 SQL Server 移轉小幫手
[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 移轉小幫手 (SSMA) 的存取是移轉工具從資料庫[!INCLUDE[msCoName](../../includes/msconame_md.md)]存取版本 97 到 2010年[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005年 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008年 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012年 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014年 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016年 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2017 在 Windows 和 Linux （預覽） / [!INCLUDE[msCoName](../../includes/msconame_md.md)] Azure SQL DB。 SSMA for Access 會將轉換至 Access 資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL 資料庫物件，這些物件組成的載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL，然後移轉資料，從存取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL。  
  
本文件介紹 SSMA for Access，並提供逐步指示，將 Access 資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 並在移轉後可能會發生問題的相關資訊。  
  
## <a name="contents"></a>目錄  
  
|章節|描述|  
|-----------|---------------|  
|[SSMA for Access 的新功能](http://msdn.microsoft.com/a24d3fc0-6911-4bfa-828a-197abf222e02)|列出 SSMA 版本所做的變更。|  
|[安裝 SQL Server 移轉小幫手，存取](installing-sql-server-migration-assistant-for-access-accesstosql.md)|列出安裝 SSMA，如需安裝和授權 SSMA，以及最新版本的連結的程序的必要條件。|  
|[Getting Started with SQL Server 移轉小幫手，存取&#40;AccessToSQL&#41;](../../ssma/access/getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)|介紹 SSMA 和其使用者介面。|  
|[準備移轉的 Access 資料庫](preparing-access-databases-for-migration-accesstosql.md)|描述如何準備您的 Access 資料庫轉換成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SQL Azure。|  
|[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)|提供轉換程序和程序中的每個步驟的詳細的資訊的概觀。|  
|[連結到 SQL Server 的 Access 應用程式](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)|描述如何使用您現有的 Access 應用程式，搭配[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|[使用者介面參考](user-interface-reference-accesstosql.md)|包含文件 SSMA 對話方塊。|  
|[使用 SSMA for Access 主控台](working-with-ssma-for-access-console-accesstosql.md)|包含在 SSMA 主控台應用程式上的文件|  
|[取得 SSMA 協助進行存取](http://go.microsoft.com/fwlink/?LinkID=708538&clcid=0x409)|提供取得其他協助的相關資訊。|  
  
