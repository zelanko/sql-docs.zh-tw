---
title: "SSMA 安裝 MySQL 用戶端 (MySQLToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Installing client,Licensing
ms.assetid: ede3128c-370d-45a5-a815-3d94eecaea30
caps.latest.revision: 22
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: eafef1f4a4f16f704b76b31aa77d3c93f84d5821
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="installing-ssma-for-mysql-client-mysqltosql"></a>安裝的 SSMA for MySQL 用戶端 (MySQLToSQL)
SSMA for MySQL 用戶端包含的程式檔案，執行下列工作：  
  
-   連接到 MySQL 資料庫。  
  
-   連接到的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。  
  
-   將 MySQL 資料庫物件，以[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 物件。  
  
-   物件載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。  
  
-   將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。  
  
本主題提供的安裝必要條件和安裝 SSMA for MySQL 用戶端的指示。  
  
## <a name="prerequisites"></a>필수 구성 요소  
SSMA for MySQL 被為了搭配 MySQL 4.1 或更新版本以及所有版本的 SQL Server 2005、 SQL Server 2008、 SQL Server 2012、 SQL Server 2014、 SQL Server 2016 和 Azure SQL DB。  
  
SSMA 安裝之前，請確定電腦符合下列需求：  
  
-   Windows 7 或更新版本中，或 Windows Server 2008 或更新版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 或更新版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 4.0 版或更新版本。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)]版本 4.0 是 SQL Server 產品媒體上的可用。 您也可以取得從[.NET Framework 開發人員中心](http://go.microsoft.com/fwlink/?LinkId=48882)。  
  
-   MySQL ODBC 5.1 驅動程式，您想要移轉的 MySQL 資料庫的連接能力。 您可以從 MySQL 網站安裝 MySQL。 如需連線資訊，請參閱[連接到 MySQL &#40;MySQLToSQL &#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
-   存取和裝載 SQL Server，您將資料庫物件和資料移轉的目標執行個體的電腦上有足夠的權限。 如需詳細資訊，請參閱[連接到 SQL Server &#40;MySQLToSQL &#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
-   發生 SQL Azure 專案的存取權以及足夠的權限的執行個體將會移轉您的 Azure SQL DB 資料庫物件和資料。 如需詳細資訊，請參閱[連接到 Azure SQL DB &#40;MySQLToSQL &#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md).  
  
-   4 GB RAM，建議使用。  
  
## <a name="installing-ssma-for-mysql-client"></a>安裝的 SSMA for MySQL 用戶端  
SSMA 是 Web 下載項目。 若要下載最新版本，請參閱[SQL Server 移轉小幫手的下載頁面](http://aka.ms/ssmaformysql)。  
  
下載最新版本之後，您必須先解壓縮安裝檔案，才能安裝 SSMA。  
  
**SSMA 用戶端安裝**  
  
1.  按兩下 SSMA for MySQL  *n* 。Install.exe 其中 *n* 是組建編號。  
  
2.  在 歡迎使用 頁面上，按一下 **下一步**。  
  
    如果您沒有安裝必要元件，會出現訊息，指出您必須先安裝必要的元件。 請確定您已安裝所有必要條件，才能再次執行安裝程式。  
  
3.  閱讀使用者授權合約。 如果您同意，請選取**我接受授權合約中的條款**，然後按一下 **下一步**。  
  
4.  在 選擇安裝類型 頁面上，按一下 **一般**。  
  
5.  按一下 **[安裝]**。  
  
> [!IMPORTANT]  
> 1.  請解除安裝所有舊版的 SSMA for MySQL 再安裝新版本。  
  
預設安裝位置是 C:\Program Files\Microsoft SQL Server 移轉小幫手的 MySQL。  
  
64 位元 Windows 電腦上已在 C:\Microsoft SQL Server 移轉小幫手的 MySQL 安裝產品。  
  
## <a name="see-also"></a>另請參閱  
[將 MySQL 資料庫移轉至 SQL Server-Azure SQL DB &#40;MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  

