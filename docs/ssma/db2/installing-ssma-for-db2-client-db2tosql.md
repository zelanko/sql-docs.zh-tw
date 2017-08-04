---
title: "SSMA 安裝 DB2 用戶端 (DB2ToSQL) |Microsoft 文件"
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
ms.assetid: 3ae2a470-6afd-4512-b6d1-fcbe6afe88ad
caps.latest.revision: 8
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4e003c72b6fea28c3048384701f3dc8839faacce
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="installing-ssma-for-db2-client-db2tosql"></a>安裝的 SSMA for DB2 用戶端 (DB2ToSQL)
SSMA 用戶端包含的程式檔案，執行下列工作：  
  
-   連接到 DB2 資料庫。  
  
-   連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 的執行個體。  
  
-   轉換至 DB2 資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]語法。  
  
-   物件載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
-   將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
本主題提供的安裝必要條件和安裝 SSMA 的指示。  
  
## <a name="prerequisites"></a>필수 구성 요소  
SSMA 設計用於 z/OS 9.0 以及 10.0 的版本上的 DB2 或 LUW 9.8 和 10.1 或更新版本上的 DB2 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2012年和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2014年。  
  
SSMA 安裝之前，請確定電腦符合下列需求：  
  
-   Windows 7 或更新版本中，或 Windows Server 2008 或更新版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 或更新版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 4.0 版或更新版本。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 4.0 版位於[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]產品媒體。 您也可以取得從[.NET Framework 開發人員中心](http://go.microsoft.com/fwlink/?LinkId=48882)。  
  
-   Microsoft OLEDB Provider for DB2 版本 5 或更新的版本，以及您想要移轉的 DB2 資料庫的連接能力。  
  
-   存取和裝載目標執行個體的電腦上有足夠的權限[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或其中您將會資料庫物件和資料移轉的 Azure SQL DB。 如需詳細資訊，請參閱[連接到 SQL Server &#40; DB2eToSQL &#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md)。  
  
-   4 GB RAM，建議使用。  
  
## <a name="microsoft-oledb-provider-for-db2"></a>Microsoft OLEDB Provider for DB2  
若要下載的 OLEDB provider for DB2 5.0 版，請移至[Microsoft® SQL Server® 2014年功能套件](http://www.microsoft.com/download/details.aspx?id=42295)。  
  
SSMA 是 Web 下載項目。 若要下載最新版本，請參閱[SQL Server 移轉小幫手的下載頁面](http://aka.ms/ssmafordb2)。  
  
下載最新版本之後，您必須先擷取中的安裝檔案，才能安裝 SSMA。  
  
**SSMA 用戶端安裝**  
  
1.  按兩下 SSMA for DB2  *n* 。Install.exe 其中 *n* 是組建編號。  
  
2.  在 歡迎使用 頁面上，按一下 **下一步**。  
  
    如果您沒有安裝必要元件，會出現訊息，指出您必須先安裝必要的元件。 請確定已安裝所有先決條件，，然後再次執行安裝程式。  
  
3.  閱讀使用者授權合約。 如果您同意，請選取**我接受授權合約中的條款**，然後按一下 **下一步**。  
  
4.  在 選擇安裝類型 頁面上，按一下 **一般**。  
  
5.  按一下 **[安裝]**。  
  
> [!IMPORTANT]  
> 1.  請先解除安裝所有舊版的 SSMA for DB2 安裝新版本之前。  
  
預設安裝位置是 C:\Program Files\Microsoft SQL Server 移轉小幫手 for DB2。  
  
## <a name="see-also"></a>另請參閱  
[SSMA 元件安裝 SQL Server &#40; DB2ToSQL &#41;](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
[DB2 資料庫移轉至 SQL Server &#40; DB2ToSQL &#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  

