---
title: 安裝 SSMA for MySQL 用戶端 (MySQLToSQL) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 1d9317b63b01a4d1e78f5c8d4818c63d9974be4f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63187195"
---
# <a name="installing-ssma-for-mysql-client-mysqltosql"></a>安裝 SSMA for MySQL 用戶端 (MySqlToSql)
SSMA for MySQL 用戶端是由執行下列工作的程式檔案所組成：  
  
-   連線到 MySQL 資料庫。  
  
-   連接到的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。  
  
-   將 MySQL 資料庫物件，以轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 物件。  
  
-   載入到物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。  
  
-   將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。  
  
本主題提供的安裝必要條件和指示安裝 SSMA for MySQL 用戶端。  
  
## <a name="prerequisites"></a>先決條件  
SSMA for MySQL 被設計用於搭配 MySQL 4.1 或更新版本以及所有版本的 SQL Server 2005、 SQL Server 2008，SQL Server 2012、 SQL Server 2014、 SQL Server 2016，SQL Server 2017 和 Azure SQL DB。  
  
安裝 SSMA 之前，請確定電腦符合下列需求：  
  
-   Windows 7 或更新版本中，或 Windows Server 2008 或更新版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 或更新版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 4.0 版或更新版本。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)]版本 4.0 是 SQL Server 產品媒體上。 您也可以取得從中[.NET Framework Developer Center](https://go.microsoft.com/fwlink/?LinkId=48882)。  
  
-   MySQL ODBC 5.1 驅動程式和連線到您想要移轉的 MySQL 資料庫。 您可以從 MySQL 網站安裝 MySQL。 如需連線資訊，請參閱[連接至 MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
-   存取並在裝載 SQL Server，您將移轉的資料庫物件和資料的目標執行個體的電腦上有足夠的權限。 如需詳細資訊，請參閱 <<c0> [ 連接到 SQL Server &#40;MySQLToSQL&#41;</c0>](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
-   SQL Azure 專案的情況下存取及足夠的權限，將會移轉您的 Azure SQL DB 執行個體資料庫物件和資料。 如需詳細資訊，請參閱 <<c0> [ 連線到 Azure SQL DB &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)。</c0>  
  
-   4 GB RAM，建議。  
  
## <a name="installing-ssma-for-mysql-client"></a>安裝 SSMA for MySQL 用戶端  
SSMA 是 Web 下載項目。 若要下載最新版本，請參閱[SQL Server Migration Assistant 的下載頁面](https://aka.ms/ssmaformysql)。  
  
下載最新版本之後，您必須先解壓縮安裝檔案，才能安裝 SSMA。  
  
**安裝 SSMA 用戶端**  
  
1.  按兩下 SSMA for MySQL *n*。Install.exe，其中*n*是組建編號。  
  
2.  在 歡迎使用 頁面上，按一下**下一步**。  
  
    如果您沒有安裝必要元件，會出現訊息，指出您必須先安裝必要的元件。 請確定您已安裝所有必要條件才能再次執行安裝程式。  
  
3.  閱讀使用者授權合約。 如果您同意，請選取**我接受授權合約中的條款**，然後按一下**下一步**。  
  
4.  在 [選擇安裝類型] 頁面上，按一下**典型**。  
  
5.  按一下 **[安裝]** 。  
  
> [!IMPORTANT]  
> 1.  請先解除安裝所有舊版的 SSMA for MySQL 才能安裝新版本。  
  
預設安裝位置是 C:\Program Files\Microsoft SQL Server Migration Assistant for MySQL。  
  
64 位元 Windows 電腦上已在 C:\Microsoft SQL Server Migration Assistant 中適用於 MySQL 安裝產品。  
  
## <a name="see-also"></a>另請參閱  
[移轉 MySQL 資料庫到 SQL Server-Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
