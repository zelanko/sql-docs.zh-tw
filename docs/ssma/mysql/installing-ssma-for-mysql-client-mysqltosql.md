---
title: 安裝 SSMA for MySQL 用戶端（MySQLToSQL） |Microsoft Docs
description: 瞭解適用于 MySQL 用戶端的 SQL Server 移轉小幫手（SSMA）安裝必要條件，以及如何安裝。
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Installing client,Licensing
ms.assetid: ede3128c-370d-45a5-a815-3d94eecaea30
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: bf1a3c8c5a01bb2553f773d5b650805667c116a3
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84293895"
---
# <a name="installing-ssma-for-mysql-client-mysqltosql"></a>安裝 SSMA for MySQL 用戶端 (MySqlToSql)
SSMA for MySQL 用戶端是由執行下列工作的程式檔案所組成：  
  
-   連接到 MySQL 資料庫。  
  
-   連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 的實例。  
  
-   將 MySQL 資料庫物件轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 物件。  
  
-   將物件載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure。  
  
-   將資料移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure。  
  
本主題提供安裝適用于 MySQL 的 SSMA 用戶端的安裝必要條件和指示。  
  
## <a name="prerequisites"></a>必要條件  
適用于 MySQL 的 SSMA 是設計用來使用 MySQL 4.1 或更新版本，以及所有版本的 SQL Server 2005、SQL Server 2008、SQL Server 2012、SQL Server 2014、SQL Server 2016、SQL Server 2017 和 Azure SQL DB。  
  
安裝 SSMA 之前，請確定電腦符合下列需求：  
  
-   Windows 7 或更新版本，或 Windows Server 2008 或更新版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 或更新版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 4.0 版或更新版本。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)]4.0 版可在 SQL Server 產品媒體上取得。 您也可以從[.NET Framework 開發人員中心](https://go.microsoft.com/fwlink/?LinkId=48882)取得。  
  
-   MySQL ODBC 5.1 驅動程式，以及您要遷移之 MySQL 資料庫的連線能力。 您可以從 MySQL 網站安裝 MySQL。 如需連線能力的相關資訊，請參閱連線[至 MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
-   在裝載 SQL Server 的目標實例之電腦上存取和足夠的許可權，您將在其中遷移資料庫物件和資料。 如需詳細資訊，請參閱[連接到 SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
-   在 SQL Azure 專案中，您將會在其中遷移資料庫物件和資料之 Azure SQL DB 實例的存取權和足夠許可權。 如需詳細資訊，請參閱[連接到 AZURE SQL DB &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)。  
  
-   建議使用 4 GB 的 RAM。  
  
## <a name="installing-ssma-for-mysql-client"></a>安裝 SSMA for MySQL 用戶端  
SSMA 是 Web 下載項目。 若要下載最新版本，請參閱[SQL Server 移轉小幫手下載頁面](https://aka.ms/ssmaformysql)。  
  
下載最新版本之後，您必須先解壓縮安裝檔案，才能安裝 SSMA。  
  
**若要安裝 SSMA 用戶端**  
  
1.  按兩下 [SSMA for MySQL *n*.Install.exe]，其中*n*是組建編號。  
  
2.  在 [歡迎] 頁面中按 [下一步]****。  
  
    如果您沒有安裝必要條件，則會出現一則訊息，指出您必須先安裝必要的元件。 再次執行安裝程式之前，請確定您已安裝所有必要條件。  
  
3.  閱讀使用者授權合約。 如果您同意，請選取 **[我接受授權合約中的條款**]，然後按 **[下一步]**。  
  
4.  在 [選擇安裝類型] 頁面上，按一下 [**一般**]。  
  
5.  按一下 [安裝]  。  
  
> [!IMPORTANT]  
> 1.  安裝新版本之前，請先卸載所有舊版的 SSMA for MySQL。  
  
預設安裝位置是 MySQL 的 C:\Program Files\Microsoft SQL Server 移轉小幫手。  
  
在64位的 Windows 機器上，產品安裝在適用于 MySQL 的 C:\Microsoft SQL Server 移轉小幫手中。  
  
## <a name="see-also"></a>另請參閱  
[將 MySQL 資料庫遷移至 SQL Server-Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
