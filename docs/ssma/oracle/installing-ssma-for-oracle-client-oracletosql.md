---
title: 安裝 SSMA for Oracle 用戶端 (OracleToSQL) |Microsoft Docs
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
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/16/2019
ms.locfileid: "68259684"
---
# <a name="installing-ssma-for-oracle-client-oracletosql"></a>安裝 SSMA for Oracle 用戶端 (OracleToSQL)
SSMA 用戶端是由執行下列工作的程式檔案所組成：  
  
-   連接到 Oracle 資料庫。  
  
-   連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。  
  
-   將 Oracle 資料庫物件，以轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]語法。  
  
-   載入到物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
-   將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
本主題提供的安裝必要條件和安裝 SSMA 的指示。  
  
## <a name="prerequisites"></a>必要條件  
SSMA 設計用於搭配 Oracle 9 或更新版本以及所有版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
安裝 SSMA 之前，請確定電腦符合下列需求：  
  
-   Windows 7 或更新版本中，或 Windows Server 2008 或更新版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 或更新版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 4.0 版或更新版本。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 4.0 版位於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]產品媒體。 您也可以取得從中[.NET Framework Developer Center](https://go.microsoft.com/fwlink/?LinkId=48882)。  
  
-   Oracle 用戶端 9.0 或更新版本，並連線到您想要移轉的 Oracle 資料庫。 Oracle 用戶端版本必須是相同的版本或更新版本的 Oracle 資料庫版本比。  
  
    從 Oracle 產品媒體或從 Oracle 網站，您可以安裝 Oracle 用戶端。 如需連線資訊，請參閱[連接到 Oracle 資料庫&#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md)。  
  
-   若要存取和裝載目標執行個體的電腦上有足夠的權限[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB，您將移轉的資料庫物件和資料。 如需詳細資訊，請參閱 <<c0> [ 連接到 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)。</c0>  
  
-   4 GB RAM，建議。  
  
## <a name="installing-the-ssma-for-oracle-client"></a>安裝 SSMA for Oracle 用戶端  
SSMA 是 Web 下載項目。 若要下載最新版本，請參閱[SQL Server Migration Assistant 的下載頁面](https://aka.ms/ssmafororacle)。  
  
下載最新版本之後，您必須先解壓縮安裝檔案，才能安裝 SSMA。  
  
**安裝 SSMA 用戶端**  
  
1.  按兩下 SSMA for Oracle *n*。Install.exe，其中*n*是組建編號。  
  
2.  在 歡迎使用 頁面上，按一下**下一步**。  
  
    如果您沒有安裝必要元件，會出現訊息，指出您必須先安裝必要的元件。 請確定您已安裝所有必要條件，然後再次執行安裝程式。  
  
3.  閱讀使用者授權合約。 如果您同意，請選取**我接受授權合約中的條款**，然後按一下**下一步**。  
  
4.  在 [選擇安裝類型] 頁面上，按一下**典型**。  
  
5.  按一下 **[安裝]** 。  
  
> [!IMPORTANT]  
> 1.  請安裝新版本之前，解除安裝所有舊版的 SSMA for Oracle。  
  
預設安裝位置是 C:\Program Files\Microsoft SQL Server Migration Assistant for Oracle。  
  
SSMA 程式除了檔案之外，您也必須安裝 SSMA for Oracle 延伸模組組件上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需詳細資訊，請參閱 < [SQL Server 上安裝 SSMA 元件&#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)。  
  
## <a name="see-also"></a>另請參閱  
[SQL Server 上安裝 SSMA 元件&#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[移轉的 Oracle 資料庫到 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
