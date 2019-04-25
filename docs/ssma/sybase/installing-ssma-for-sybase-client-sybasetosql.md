---
title: 安裝 SSMA for Sybase (Sybasetosql) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: e770c2f2-52b9-4471-a207-0d35df41399c
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 6cca10f2a54a70e91e46bb8b98e9799885b5f175
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62740988"
---
# <a name="installing-ssma--for-sybase-client-sybasetosql"></a>安裝 SSMA for Sybase (SybaseToSQL)
SSMA 用戶端包含用來連接到 Sybase Adaptive Server Enterprise (ASE) 的資料庫伺服器和執行個體的程式檔案[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB，ASE 資料庫物件，以轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB 語法，載入物件組成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB，然後再移轉資料至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQLDB。  
  
本主題提供的安裝必要條件和安裝 SSMA 的指示。  
  
## <a name="prerequisites"></a>先決條件  
SSMA 設計用於搭配 ASE 11.9.2 或更新版本以及所有版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
安裝 SSMA 之前，請確定電腦符合下列需求：  
  
-   Windows 7 或更新版本中，或 Windows Server 2008 或更新版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 或更新版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] .NET Framework 4.0 版或更新版本。 .NET Framework 4.0 版位於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]產品媒體。 您也可以取得從中[.NET Framework Developer Center](https://go.microsoft.com/fwlink/?LinkId=48882)。  
  
-   Sybase OLEDB/ADO.Net/ODBC 提供者和連線到 Sybase ASE 資料庫伺服器，其中包含您想要移轉的資料庫。 您可以從 Sybase ASE 產品媒體安裝提供者。 如需連線資訊，請參閱[連接到 Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)。  
  
-   若要存取和裝載目標執行個體的電腦上有足夠的權限[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB，您將移轉的資料庫物件和資料。 如需詳細資訊，請參閱[連線到 SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md)/[Azure SQL 資料庫連線&#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)。  
  
-   4 GB RAM，建議。  
  
## <a name="installing-the-ssma-for-sybase-client"></a>安裝 SSMA for Sybase 用戶端  
SSMA 是 Web 下載項目。 若要下載最新版本，請參閱[SQL Server Migration Assistant 的下載頁面](https://aka.ms/ssmaforsybase)。  
  
下載最新版本之後，您必須先解壓縮安裝檔案，才能安裝 SSMA。  
  
**安裝 SSMA 用戶端**  
  
1.  按兩下 SSMA for Sybase *n*。Install.exe，其中*n*是組建編號。  
  
2.  在 歡迎使用 頁面上，按一下**下一步**。  
  
    如果您沒有安裝必要元件，會出現訊息，指出您必須先安裝必要的元件。 請確定您已安裝所有必要條件，然後再次執行安裝程式。  
  
3.  閱讀使用者授權合約。 如果您同意，請選取**我接受授權合約中的條款**，然後按一下**下一步**。  
  
4.  在 [選擇安裝類型] 頁面上，按一下**典型**。  
  
5.  按一下 **[安裝]**。  
  
> [!IMPORTANT]  
> 1.  請解除安裝所有舊版的 SSMA for Sybase 才能安裝新版本。  
  
預設安裝位置是 C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase。  
  
SSMA 程式除了檔案之外，您也必須安裝 SSMA for Sybase 延伸模組套件上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需詳細資訊，請參閱 < [SQL Server 上安裝 SSMA 元件&#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)。  
  
## <a name="see-also"></a>另請參閱  
[SQL Server 上安裝 SSMA 元件&#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
[將 Sybase ASE 資料庫移轉至 SQL Server-Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
