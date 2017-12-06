---
title: "安裝 SSMA for Sybase 用戶端 (SybaseToSQL) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-sybase
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: e770c2f2-52b9-4471-a207-0d35df41399c
caps.latest.revision: "18"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d7fe5ff03fd5f16700480bdb11b3fd8f45a51ccc
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="installing-ssma--for-sybase-client-sybasetosql"></a>安裝的 SSMA for Sybase 用戶端 (SybaseToSQL)
SSMA 用戶端所組成，可用來連接到 Sybase Adaptive Server Enterprise (ASE) 資料庫伺服器和執行個體的程式檔案[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或轉換至 ASE 資料庫物件的 Azure SQL DB[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB 語法，物件載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB、，然後將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQLDB。  
  
本主題提供的安裝必要條件和安裝 SSMA 的指示。  
  
## <a name="prerequisites"></a>必要條件  
SSMA 設計來搭配 ASE 11.9.2 或更新版本以及所有版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
SSMA 安裝之前，請確定電腦符合下列需求：  
  
-   Windows 7 或更新版本中，或 Windows Server 2008 或更新版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 或更新版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] .NET Framework 4.0 版或更新版本。 .NET Framework 4.0 版位於[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]產品媒體。 您也可以取得從[.NET Framework 開發人員中心](http://go.microsoft.com/fwlink/?LinkId=48882)。  
  
-   Sybase OLEDB/ADO.Net/ODBC 提供者和連接至 Sybase ASE 資料庫伺服器，其中包含您想要移轉的資料庫。 您可以從 Sybase ASE 產品媒體安裝提供者。 如需連線資訊，請參閱[連接到 Sybase ASE &#40;SybaseToSQL &#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md).  
  
-   存取和裝載目標執行個體的電腦上有足夠的權限[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或其中您將會資料庫物件和資料移轉的 Azure SQL DB。 如需詳細資訊，請參閱[連接到 SQL Server &#40;SybaseToSQL &#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md) /[連接到 Azure SQL DB &#40;SybaseToSQL &#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md).  
  
-   4 GB RAM，建議使用。  
  
## <a name="installing-the-ssma-for-sybase-client"></a>安裝的 SSMA for Sybase 用戶端  
SSMA 是 Web 下載項目。 若要下載最新版本，請參閱[SQL Server 移轉小幫手的下載頁面](http://aka.ms/ssmaforsybase)。  
  
下載最新版本之後，您必須先擷取中的安裝檔案，才能安裝 SSMA。  
  
**SSMA 用戶端安裝**  
  
1.  按兩下 SSMA for Sybase  *n* 。Install.exe 其中 *n* 是組建編號。  
  
2.  在 歡迎使用 頁面上，按一下 **下一步**。  
  
    如果您沒有安裝必要元件，會出現訊息，指出您必須先安裝必要的元件。 請確定已安裝所有先決條件，，然後再次執行安裝程式。  
  
3.  閱讀使用者授權合約。 如果您同意，請選取**我接受授權合約中的條款**，然後按一下 **下一步**。  
  
4.  在 選擇安裝類型 頁面上，按一下 **一般**。  
  
5.  按一下 **[安裝]**。  
  
> [!IMPORTANT]  
> 1.  請解除安裝所有舊版的 SSMA for Sybase 再安裝新版本。  
  
預設安裝位置是 C:\Program Files\Microsoft SQL Server 移轉小幫手 Sybase 的。  
  
SSMA 程式除了檔案之外，您也必須安裝 SSMA for Sybase 延伸模組組件上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 如需詳細資訊，請參閱[上 SQL Server &#40; 安裝 SSMA 元件SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md).  
  
## <a name="see-also"></a>請參閱  
[在 SQL Server &#40; 安裝 SSMA 元件SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
[Sybase ASE 將資料庫移轉至 SQL Server-Azure SQL DB &#40;SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
