---
title: 安裝適用于 Sybase 用戶端的 SSMA （SybaseToSQL） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: e770c2f2-52b9-4471-a207-0d35df41399c
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 8680685640b234e47f6e68d7fb802fc7e2f5d81c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68029017"
---
# <a name="installing-ssma--for-sybase-client-sybasetosql"></a>安裝 SSMA for Sybase (SybaseToSQL)
SSMA 客戶[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]端包含用來連接到 Sybase 調適型伺服器 ENTERPRISE （ASE）資料庫伺服器和實例或 AZURE sql db 的程式檔案、將 ASE 資料庫物件轉換成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 azure sql db 語法、將物件載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 azure sql db，然後將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 azure SQLDB。  
  
本主題提供安裝 SSMA 的必要條件和指示。  
  
## <a name="prerequisites"></a>Prerequisites  
SSMA 是設計用來搭配 ASE 11.9.2 或更新版本，以及的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所有版本。  
  
安裝 SSMA 之前，請確定電腦符合下列需求：  
  
-   Windows 7 或更新版本，或 Windows Server 2008 或更新版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 或更新版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] .NET Framework 版本4.0 或更新版本。 .NET Framework 版本4.0 可在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]產品媒體上取得。 您也可以從[.NET Framework 開發人員中心](https://go.microsoft.com/fwlink/?LinkId=48882)取得。  
  
-   Sybase OLEDB/ADO.Net/ODBC 提供者，以及包含您想要遷移之資料庫的 Sybase ASE 資料庫伺服器的連接。 您可以從 Sybase ASE 產品媒體安裝提供者。 如需連線的詳細資訊，請參閱[連接到 SYBASE ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)。  
  
-   在裝載目標實例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 AZURE SQL DB 的電腦上存取和足夠的許可權，您將在其中遷移資料庫物件和資料。 如需詳細資訊，請參閱連接到[SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md) /[連接到 Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)。  
  
-   建議使用 4 GB 的 RAM。  
  
## <a name="installing-the-ssma-for-sybase-client"></a>安裝適用于 Sybase 用戶端的 SSMA  
SSMA 是 Web 下載項目。 若要下載最新版本，請參閱[SQL Server 移轉小幫手下載頁面](https://aka.ms/ssmaforsybase)。  
  
下載最新版本之後，您必須先從解壓縮安裝檔案，才能安裝 SSMA。  
  
**若要安裝 SSMA 用戶端**  
  
1.  按兩下 [SSMA] 做為 [Sybase *n*]。安裝 .exe，其中*n*是組建編號。  
  
2.  在 [歡迎] 頁面中按 [下一步]****。  
  
    如果您未安裝必要條件，則會出現一則訊息，指出您必須先安裝必要的元件。 請確定您已安裝所有必要條件，然後再次執行安裝程式。  
  
3.  閱讀使用者授權合約。 如果您同意，請選取 **[我接受授權合約中的條款**]，然後按 **[下一步]**。  
  
4.  在 [選擇安裝類型] 頁面上，按一下 [**一般**]。  
  
5.  按一下 [Install]  。  
  
> [!IMPORTANT]  
> 1.  請先卸載所有先前版本的 SSMA for Sybase，再安裝新版本。  
  
預設安裝位置是 Sybase 的 C:\Program Files\Microsoft SQL Server 移轉小幫手。  
  
除了 SSMA 程式檔案之外，您還必須在上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝適用于 Sybase 擴充功能套件的 SSMA。 如需詳細資訊，請參閱[在 SQL Server &#40;SybaseToSQL&#41;上安裝 SSMA 元件](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)。  
  
## <a name="see-also"></a>另請參閱  
[在 SQL Server &#40;SybaseToSQL 上安裝 SSMA 元件&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
[將 Sybase ASE 資料庫移轉至 SQL Server-Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
