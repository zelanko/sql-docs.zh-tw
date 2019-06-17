---
title: 安裝 SSMA for DB2 用戶端 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 3ae2a470-6afd-4512-b6d1-fcbe6afe88ad
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 1d479c8f7de1c9d7463e57f37f9e8588c9bc68b6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63299044"
---
# <a name="installing-ssma-for-db2-client-db2tosql"></a>安裝 SSMA for DB2 用戶端 (DB2ToSQL)
SSMA 用戶端是由執行下列工作的程式檔案所組成：  
  
-   連接到 DB2 資料庫。  
  
-   連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。  
  
-   轉換到 DB2 資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]語法。  
  
-   載入到物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
-   將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
本主題提供的安裝必要條件和安裝 SSMA 的指示。  
  
## <a name="prerequisites"></a>先決條件  
SSMA 設計用於搭配 z/OS 9.0 以及 10.0 的版本上的 DB2 或 LUW 版本 9.8 和 10.1 或更新版本的 DB2 及[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012年和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014年。  
  
安裝 SSMA 之前，請確定電腦符合下列需求：  
  
-   Windows 7 或更新版本中，或 Windows Server 2008 或更新版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 或更新版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 4.0 版或更新版本。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 4.0 版位於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]產品媒體。 您也可以取得從中[.NET Framework Developer Center](https://go.microsoft.com/fwlink/?LinkId=48882)。  
  
-   Microsoft OLEDB Provider for DB2 第 5 版或更新版本，並連線到您想要移轉的 DB2 資料庫。  
  
-   若要存取和裝載目標執行個體的電腦上有足夠的權限[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB，您將移轉的資料庫物件和資料。 如需詳細資訊，請參閱 <<c0> [ 連接到 SQL Server &#40;DB2eToSQL&#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md)。</c0>  
  
-   4 GB RAM，建議。  
  
## <a name="microsoft-oledb-provider-for-db2"></a>Microsoft OLEDB Provider for DB2  
若要下載的 OLEDB provider for DB2 5.0 版，請移至[Microsoft® SQL Server® 2014 Feature Pack](https://www.microsoft.com/download/details.aspx?id=42295)。  
  
SSMA 是 Web 下載項目。 若要下載最新版本，請參閱[SQL Server Migration Assistant 的下載頁面](https://aka.ms/ssmafordb2)。  
  
下載最新版本之後，您必須先解壓縮安裝檔案，才能安裝 SSMA。  
  
**安裝 SSMA 用戶端**  
  
1.  按兩下 SSMA for DB2 *n*。Install.exe，其中*n*是組建編號。  
  
2.  在 歡迎使用 頁面上，按一下**下一步**。  
  
    如果您沒有安裝必要元件，會出現訊息，指出您必須先安裝必要的元件。 請確定您已安裝所有必要條件，然後再次執行安裝程式。  
  
3.  閱讀使用者授權合約。 如果您同意，請選取**我接受授權合約中的條款**，然後按一下**下一步**。  
  
4.  在 [選擇安裝類型] 頁面上，按一下**典型**。  
  
5.  按一下 **[安裝]** 。  
  
> [!IMPORTANT]  
> 1.  請先解除安裝所有舊版的 SSMA for DB2 才能安裝新版本。  
  
預設安裝位置是 C:\Program Files\Microsoft SQL Server Migration Assistant for DB2。  
  
## <a name="see-also"></a>另請參閱  
[SQL Server 上安裝 SSMA 元件&#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
[移轉的 DB2 資料庫到 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
