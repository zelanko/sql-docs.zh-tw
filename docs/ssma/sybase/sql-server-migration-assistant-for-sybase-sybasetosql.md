---
title: Sybase 的 SQL Server 移轉小幫手（SybaseToSQL） |Microsoft Docs
description: 瞭解適用于 Sybase 的 SSMA，並遵循將 ASE 資料庫移轉至 SQL Server 或 Azure SQL Database 的逐步指示。
ms.custom: ''
ms.date: 10/10/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 59e63eac-8a7e-4d54-be1c-0633a9bf510d
author: Jtoland
ms.author: Jtoland
manager: murato
ms.openlocfilehash: 269fa36b578b7b13d12d5b6fd9645e84c7c39244
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84293985"
---
# <a name="sql-server-migration-assistant-for-sybase-sybasetosql"></a>Sybase 的 SQL Server 移轉小幫手（SybaseToSQL）

[!INCLUDE[msCoName](../../includes/msconame_md.md)]適用于 Sybase 調適型 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 伺服器 Enterprise （ASE）的移轉小幫手（SSMA）是將 ASE 資料庫移轉至 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的工具2012、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] windows 和 linux 上的2017、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] windows 和 linux 上的2019，或 [!INCLUDE[msCoName](../../includes/msconame_md.md)] Azure SQL Database。 SSMA for Sybase 會將 ASE 資料庫物件轉換為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫物件、在或 Azure SQL Database 中建立這些物件 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，然後將 ase 中的資料移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database。
  
本檔將為您介紹 SSMA for Sybase，並提供將 ASE 資料庫移轉至或 Azure SQL Database 的逐步指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，以及有關遷移後可能發生之問題的資訊。 若要深入瞭解，請參閱下列文章。  
  
## <a name="contents"></a>目錄  
  
|區段|Description|
|-----------|---------------|
|[SSMA for Sybase 的新功能 &#40;SybaseToSQL&#41;](../../ssma/sybase/what-s-new-in-ssma-for-sybase-sybasetosql.md)|列出 SSMA 版本的變更。|  
|[安裝 SSMA for Sybase &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)|包含的文章會提供必要條件，以及在執行實例的電腦上安裝 SSMA for Sybase 用戶端和必要元件的指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|[適用于 Sybase &#40;SybaseToSQL 的 SSMA 消費者入門&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)|介紹使用者介面、專案和設定選項。|  
|[將 Sybase ASE 資料庫移轉至 SQL Server-Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)|提供轉換程式的總覽，以及處理常式中每個步驟的詳細資訊。|  
|[&#40;SybaseToSQL&#41;的使用者介面參考](../../ssma/sybase/user-interface-reference-sybasetosql.md)|包含適用于 Sybase 對話方塊的 SSMA 檔。|  
|[使用 SSMA for Sybase 主控台](working-with-ssma-for-sybase-console-sybasetosql.md)|包含 SSMA 主控台應用程式的相關檔。|  
|[取得 Sybase 協助的 SSMA](https://go.microsoft.com/fwlink/?LinkID=708538&clcid=0x409)|提供有關取得其他協助的資訊。|  
