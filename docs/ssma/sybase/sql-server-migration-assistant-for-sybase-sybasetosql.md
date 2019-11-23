---
title: Sybase 的 SQL Server 移轉小幫手（SybaseToSQL） |Microsoft Docs
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
ms.openlocfilehash: 3913ae22155ca5e560db7fee946df0f8062a23b9
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252161"
---
# <a name="sql-server-migration-assistant-for-sybase-sybasetosql"></a>Sybase 的 SQL Server 移轉小幫手（SybaseToSQL）

適用于 Sybase 調適型伺服器 Enterprise （ASE）的 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 移轉小幫手（SSMA）是一種工具，可將 ASE 資料庫移轉至 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012、[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014、[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016、[!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows 和 Linux 上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2017、在 Windows 和 linux 上 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2019，或 [!INCLUDE[msCoName](../../includes/msconame_md.md)] Azure SQL Database。 SSMA for Sybase 會將 ASE 資料庫物件轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫物件、在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database 中建立這些物件，然後將 ASE 中的資料移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database。
  
本檔將為您介紹 SSMA for Sybase，並提供將 ASE 資料庫移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database 的逐步指示，以及有關遷移後可能發生之問題的資訊。 若要深入瞭解，請參閱下列文章。  
  
## <a name="contents"></a>目錄  
  
|章節|描述|
|-----------|---------------|
|[SSMA for Sybase &#40;SybaseToSQL 的新功能&#41;](../../ssma/sybase/what-s-new-in-ssma-for-sybase-sybasetosql.md)|列出 SSMA 版本的變更。|  
|[安裝 SSMA for Sybase &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)|包含的文章提供必要條件和指示，說明如何在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 實例的電腦上安裝 Sybase 用戶端和必要元件的 SSMA。|  
|[SSMA for Sybase &#40;SybaseToSQL 的消費者入門&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)|介紹使用者介面、專案和設定選項。|  
|[將 Sybase ASE 資料庫移轉至 SQL Server-Azure SQL &#40;DB SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)|提供轉換程式的總覽，以及處理常式中每個步驟的詳細資訊。|  
|[使用者介面參考&#40;SybaseToSQL&#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)|包含適用于 Sybase 對話方塊的 SSMA 檔。|  
|[使用 SSMA for Sybase 主控台](working-with-ssma-for-sybase-console-sybasetosql.md)|包含 SSMA 主控台應用程式的相關檔。|  
|[取得 Sybase 協助的 SSMA](https://go.microsoft.com/fwlink/?LinkID=708538&clcid=0x409)|提供有關取得其他協助的資訊。|  
