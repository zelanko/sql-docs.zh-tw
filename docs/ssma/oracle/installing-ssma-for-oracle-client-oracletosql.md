---
title: 安裝 SSMA for Oracle 用戶端（OracleToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Licensing SSMA
ms.assetid: d5d4903d-e296-4bbf-8780-63674c4d62d5
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: fc295e108357040617bf6bdaa1af61fada2c97ee
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68259684"
---
# <a name="installing-ssma-for-oracle-client-oracletosql"></a>安裝 SSMA for Oracle 用戶端 (OracleToSQL)
SSMA 用戶端是由執行下列工作的程式檔案所組成：  
  
-   連接到 Oracle 資料庫。  
  
-   連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。  
  
-   將 Oracle 資料庫物件轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]成語法。  
  
-   將物件載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
-   將資料移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]至。  
  
本主題提供安裝 SSMA 的必要條件和指示。  
  
## <a name="prerequisites"></a>Prerequisites  
SSMA 是設計用來搭配 Oracle 9 或更新版本，以及的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所有版本。  
  
安裝 SSMA 之前，請確定電腦符合下列需求：  
  
-   Windows 7 或更新版本，或 Windows Server 2008 或更新版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 或更新版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 4.0 版或更新版本。 4.0 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)]版可在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]產品媒體上取得。 您也可以從[.NET Framework 開發人員中心](https://go.microsoft.com/fwlink/?LinkId=48882)取得。  
  
-   Oracle 用戶端9.0 或更新版本，以及與您要遷移之 Oracle 資料庫的連接。 Oracle 用戶端版本必須與 Oracle 資料庫版本的版本相同或更新版本相同。  
  
    您可以從 Oracle 產品媒體或從 Oracle 網站安裝 Oracle 用戶端。 如需連線的詳細資訊，請參閱[連接到 Oracle Database &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md)。  
  
-   在裝載目標實例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 AZURE SQL DB 的電腦上存取和足夠的許可權，您將在其中遷移資料庫物件和資料。 如需詳細資訊，請參閱[連接到 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)。  
  
-   建議使用 4 GB 的 RAM。  
  
## <a name="installing-the-ssma-for-oracle-client"></a>安裝 SSMA for Oracle 用戶端  
SSMA 是 Web 下載項目。 若要下載最新版本，請參閱[SQL Server 移轉小幫手下載頁面](https://aka.ms/ssmafororacle)。  
  
下載最新版本之後，您必須先從解壓縮安裝檔案，才能安裝 SSMA。  
  
**若要安裝 SSMA 用戶端**  
  
1.  按兩下 [SSMA for Oracle *n*]。安裝 .exe，其中*n*是組建編號。  
  
2.  在 [歡迎] 頁面中按 [下一步] ****。  
  
    如果您未安裝必要條件，則會出現一則訊息，指出您必須先安裝必要的元件。 請確定您已安裝所有必要條件，然後再次執行安裝程式。  
  
3.  閱讀使用者授權合約。 如果您同意，請選取 **[我接受授權合約中的條款**]，然後按 **[下一步]**。  
  
4.  在 [選擇安裝類型] 頁面上，按一下 [**一般**]。  
  
5.  按一下 **[安裝]**。  
  
> [!IMPORTANT]  
> 1.  請先卸載所有舊版的 SSMA for Oracle，再安裝新版本。  
  
預設安裝位置為 Oracle 的 C:\Program Files\Microsoft SQL Server 移轉小幫手。  
  
除了 SSMA 程式檔案之外，您還必須在上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝 SSMA for Oracle extension pack。 如需詳細資訊，請參閱[在 SQL Server &#40;OracleToSQL&#41;上安裝 SSMA 元件](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)。  
  
## <a name="see-also"></a>另請參閱  
[在 SQL Server &#40;OracleToSQL 上安裝 SSMA 元件&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[將 Oracle 資料庫移轉至 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
