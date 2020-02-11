---
title: 適用于 MySQL 的 SQL Server 移轉小幫手（MySQLToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 10/10/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2793bc33-38d3-46ed-8277-b8580cf78ced
author: Jtoland
ms.author: Jtoland
manager: murato
ms.openlocfilehash: 61f1edc662e7b4a510d616dbee47cfaa615b9c0c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "72252148"
---
# <a name="sql-server-migration-assistant-for-mysql-mysqltosql"></a>適用于 MySQL 的 SQL Server 移轉小幫手（MySQLToSQL）

[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]適用于 mysql 的移轉小幫手（SSMA）是一種工具，可[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]將 mysql [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫移轉[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]至 2012 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、2014、2016、windows [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和 linux 上的2017、windows 和[!INCLUDE[msCoName](../../includes/msconame_md.md)] linux 上的2019，或 Azure 資料庫。 適用于 MySQL 的 SSMA 會將 MySQL 資料庫物件轉換成 SQL Server 資料庫物件、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在中建立這些物件，然後將[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料從 MySQL 遷移至。  
  
本檔將為您介紹 SSMA for MySQL，並提供將 MySQL 資料庫遷移至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的逐步指示。 下表顯示可協助您深入瞭解的文章：  
  
## <a name="contents"></a>內容  
  
|區段|描述|
|-----------|---------------|
|[SSMA for MySQL 的新功能](https://msdn.microsoft.com/1451a0b0-6713-4d0c-954f-ea3d8fce1d31)|這一版的 SSMA for MySQL 的新功能|  
|[安裝 SSMA for MySQL &#40;MySqlToSql&#41;](../../ssma/mysql/installing-ssma-for-mysql-mysqltosql.md)|包含的文章會提供必要條件和指示，說明如何在執行 SQL Server 的電腦上安裝 SSMA for MySQL 用戶端和必要元件。|  
|[適用于 MySQL 的 SSMA &#40;MySQLToSQL&#41;的消費者入門](../../ssma/mysql/getting-started-with-ssma-for-mysql-mysqltosql.md)|介紹使用者介面、專案和設定選項。|  
|[將 MySQL 資料庫遷移至 SQL Server-Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)|提供轉換程式的總覽，以及處理常式中每個步驟的詳細資訊。|  
|[&#40;MySQLToSQL&#41;的使用者介面參考](../../ssma/mysql/user-interface-reference-mysqltosql.md)|包含 [適用于 MySQL 的 SSMA] 對話方塊的檔。|  
|[使用 SSMA for MySQL 主控台](working-with-ssma-for-mysql-console-mysqltosql.md)|包含 SSMA 主控台應用程式的檔|  
|[取得 MySQL 的 SSMA 協助](https://go.microsoft.com/fwlink/?LinkID=708538&clcid=0x409)|提供有關取得其他協助的資訊。|  
