---
title: 安裝適用于 MySQL 的 SSMA 用戶端 (MySQLToSQL) |Microsoft Docs
description: 瞭解適用于 MySQL 用戶端的 SQL Server 移轉小幫手 (SSMA) 的安裝必要條件，以及如何安裝。
ms.prod: sql
ms.custom: ''
ms.date: 07/14/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Installing client,Licensing
ms.assetid: ede3128c-370d-45a5-a815-3d94eecaea30
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: d6bda2cad0761dbb53fcc4bb66d29829841f249d
ms.sourcegitcommit: 777704aefa7e574f4b7d62ad2a4c1b10ca1731ff
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2020
ms.locfileid: "87824030"
---
# <a name="installing-ssma-for-mysql-client-mysqltosql"></a>安裝適用于 MySQL 的 SSMA 用戶端 (MySQLToSQL) 

SSMA for MySQL 用戶端是由執行下列工作的程式檔案所組成：

- 連接到 MySQL 資料庫。  
- 連接到或的實例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 。
- 將 MySQL 資料庫物件轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 物件。
- 將物件載入至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 。
- 將資料移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 。

本主題提供安裝適用于 MySQL 的 SSMA 用戶端的安裝必要條件和指示。

## <a name="prerequisites"></a>必要條件

適用于 MySQL 的 SSMA 是設計來使用 MySQL 4.1 或更新版本，以及2012或更新版本的所有版本 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，以及 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 。

安裝 SSMA 之前，請確定電腦符合下列需求：

- Windows 7 或更新版本，或 Windows Server 2008 或更新版本。
- [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 或更新版本。
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 版本4.7.2 或更新版本。 您可以從[.NET Framework 開發人員中心](https://go.microsoft.com/fwlink/?LinkId=48882)取得此檔案。
- MySQL ODBC 5.1 驅動程式，以及您要遷移之 MySQL 資料庫的連線能力。 您可以從 MySQL 網站安裝 MySQL。 如需連線能力的相關資訊，請參閱連線[到 MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)。
- 在裝載 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 您要遷移資料庫物件和資料之目標實例的電腦上，存取和足夠的許可權。 如需詳細資訊，請參閱[連接到 SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)。
- 若為 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 專案，請存取 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 您將在其中遷移資料庫物件和資料之實例的足夠許可權。 如需詳細資訊，請參閱[連接到 Azure SQL Database &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)。
- 建議使用 4 GB 的 RAM。

## <a name="installing-ssma-for-mysql-client"></a>安裝 SSMA for MySQL 用戶端

SSMA 是 Web 下載項目。 若要下載最新版本，請參閱[SQL Server 移轉小幫手下載頁面](https://aka.ms/ssmaformysql)。

若要安裝 SSMA 用戶端：

1. 按兩下 [ **SSMAforMySQL_*n*.msi**]，其中*n*是組建編號。
2. 在 [歡迎] 頁面中按 [下一步]。

   如果您沒有安裝必要條件，則會出現一則訊息，指出您必須先安裝必要的元件。 再次執行安裝程式之前，請確定您已安裝所有必要條件。

3. 閱讀使用者授權合約。 如果您同意，請選取 **[我接受合約**]，然後按 **[下一步]**。
4. 在 [**選擇安裝類型**] 頁面上，按一下 [**一般**]。
5. 在 [**準備安裝**] 頁面上，您可以啟用或停用每次工具啟動時的遙測和自動更新檢查。 按一下 [安裝]**** 可開始進行安裝。

> [!IMPORTANT]
> 安裝新版本之前，請先卸載所有舊版的 SSMA for MySQL。

預設安裝位置是 `C:\Program Files\Microsoft SQL Server Migration Assistant for MySQL`。

## <a name="see-also"></a>另請參閱

- [將 MySQL 資料庫遷移至 SQL Server Azure SQL Database](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
