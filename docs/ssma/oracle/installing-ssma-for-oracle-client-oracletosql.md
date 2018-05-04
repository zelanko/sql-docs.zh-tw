---
title: SSMA 安裝 Oracle 用戶端 (OracleToSQL) |Microsoft 文件
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Licensing SSMA
ms.assetid: d5d4903d-e296-4bbf-8780-63674c4d62d5
caps.latest.revision: 19
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 33abd4c84e195760791c417b3eb629fa5af3fe01
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="installing-ssma-for-oracle-client-oracletosql"></a>安裝的 SSMA for Oracle 用戶端 (OracleToSQL)
SSMA 用戶端包含的程式檔案，執行下列工作：  
  
-   連接到 Oracle 資料庫。  
  
-   連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 的執行個體。  
  
-   將 Oracle 資料庫物件來[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]語法。  
  
-   物件載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
-   將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
本主題提供的安裝必要條件和安裝 SSMA 的指示。  
  
## <a name="prerequisites"></a>필수 구성 요소  
SSMA 設計成使用 Oracle 9 或更新版本以及所有版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
SSMA 安裝之前，請確定電腦符合下列需求：  
  
-   Windows 7 或更新版本中，或 Windows Server 2008 或更新版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 或更新版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 4.0 版或更新版本。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 4.0 版位於[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]產品媒體。 您也可以取得從[.NET Framework 開發人員中心](http://go.microsoft.com/fwlink/?LinkId=48882)。  
  
-   Oracle 用戶端 9.0 或更新版本，並連線到您想要移轉的 Oracle 資料庫。 Oracle 用戶端版本必須是相同的版本或 Oracle 資料庫版本比更新的版本。  
  
    從 Oracle 產品媒體或從 Oracle 網站，您可以安裝 Oracle 用戶端。 如需連線資訊，請參閱[連接到 Oracle 資料庫&#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md)。  
  
-   存取和裝載目標執行個體的電腦上有足夠的權限[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或其中您將會資料庫物件和資料移轉的 Azure SQL DB。 如需詳細資訊，請參閱[連接到 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)。  
  
-   4 GB RAM，建議使用。  
  
## <a name="installing-the-ssma-for-oracle-client"></a>SSMA 安裝 Oracle 用戶端  
SSMA 是 Web 下載項目。 若要下載最新版本，請參閱[SQL Server 移轉小幫手的下載頁面](http://aka.ms/ssmafororacle)。  
  
下載最新版本之後，您必須先擷取中的安裝檔案，才能安裝 SSMA。  
  
**SSMA 用戶端安裝**  
  
1.  按兩下 SSMA for Oracle *n*。Install.exe 其中*n*是組建編號。  
  
2.  在 歡迎使用 頁面上，按一下 **下一步**。  
  
    如果您沒有安裝必要元件，會出現訊息，指出您必須先安裝必要的元件。 請確定已安裝所有先決條件，，然後再次執行安裝程式。  
  
3.  閱讀使用者授權合約。 如果您同意，請選取**我接受授權合約中的條款**，然後按一下 **下一步**。  
  
4.  在 選擇安裝類型 頁面上，按一下 **一般**。  
  
5.  按一下 **[安裝]**。  
  
> [!IMPORTANT]  
> 1.  請安裝新版本之前，解除安裝所有舊版的 SSMA for Oracle。  
  
預設安裝位置是 C:\Program Files\Microsoft SQL Server 移轉小幫手 for Oracle。  
  
SSMA 程式除了檔案之外，您也必須安裝 SSMA for Oracle 延伸模組組件上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 如需詳細資訊，請參閱[安裝 SQL Server 上的 SSMA 元件&#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)。  
  
## <a name="see-also"></a>另請參閱  
[安裝 SQL Server 上的 SSMA 元件&#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[SQL server 資料庫移轉 Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
