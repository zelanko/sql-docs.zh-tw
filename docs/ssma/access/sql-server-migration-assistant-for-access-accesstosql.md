---
title: 存取的 SQL Server 移轉小幫手（AccessToSQL） |Microsoft Docs
description: 瞭解 SSMA 的存取權，並遵循將 Access 資料庫移轉至 SQL Server 或 Azure SQL Database 的逐步指示。
ms.prod: sql
ms.custom: ''
ms.date: 10/10/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 40c1eb02-26b2-44ba-969d-6c430c61c281
author: Jtoland
ms.author: Jtoland
manager: murato
ms.openlocfilehash: 2e4ce80a111efcf978da55cab280205b08acdd1f
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84292936"
---
# <a name="sql-server-migration-assistant-for-access-accesstosql"></a>存取的 SQL Server 移轉小幫手（AccessToSQL）

[!INCLUDE[msCoName](../../includes/msconame_md.md)]適用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 于 Access 的移轉小幫手（SSMA）是用來從 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 遷移資料庫的工具在 Windows 和 Linux 上存取版本97到2010至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2017、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] windows 和 linux 上的2019，或 [!INCLUDE[msCoName](../../includes/msconame_md.md)] Azure SQL Database。 SSMA for Access 會將 Access 資料庫物件轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 AZURE SQL database 物件、將這些物件載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database，然後將資料從存取權遷移至或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Azure SQL Database。
  
本檔將為您介紹 SSMA 的存取權，並提供將 Access 資料庫移轉至或 Azure SQL Database 的逐步指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，以及有關遷移後可能發生之問題的資訊。  
  
## <a name="contents"></a>目錄  
  
|區段|Description|
|-----------|---------------|
|[SSMA for Access 的新功能](https://msdn.microsoft.com/a24d3fc0-6911-4bfa-828a-197abf222e02)|列出 SSMA 版本的變更。|  
|[安裝 SQL Server 移轉小幫手以進行存取](installing-sql-server-migration-assistant-for-access-accesstosql.md)|列出安裝 SSMA 的必要條件、安裝和授權 SSMA 的程式，以及最新版本的連結。|  
|[使用 SQL Server 移轉小幫手存取 &#40;AccessToSQL 的消費者入門&#41;](../../ssma/access/getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)|引進 SSMA 及其使用者介面。|  
|[準備 Access 資料庫以進行遷移](preparing-access-databases-for-migration-accesstosql.md)|說明如何準備您的 Access 資料庫，以轉換至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure。|  
|[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)|提供轉換程式的總覽，以及處理常式中每個步驟的詳細資訊。|  
|[將存取應用程式連結至 SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)|說明如何搭配使用現有的 Access 應用程式 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|[使用者介面參考](user-interface-reference-accesstosql.md)|包含 SSMA 對話方塊的檔。|  
|[使用 SSMA for Access 主控台](working-with-ssma-for-access-console-accesstosql.md)|包含 SSMA 主控台應用程式的檔|  
|[取得存取權的 SSMA 協助](https://go.microsoft.com/fwlink/?LinkID=708538&clcid=0x409)|提供有關取得其他協助的資訊。|  
