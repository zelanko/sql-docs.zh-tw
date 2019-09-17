---
title: 安裝 SSMA for DB2 用戶端（DB2ToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 09/07/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 3ae2a470-6afd-4512-b6d1-fcbe6afe88ad
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 1623430eed752db7fa387caf33124082eb318490
ms.sourcegitcommit: 243925311cc952dd455faea3c1156e980959d6de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/07/2019
ms.locfileid: "70774189"
---
# <a name="installing-ssma-for-db2-client-db2tosql"></a>安裝 SSMA for DB2 用戶端（DB2ToSQL）

SSMA 用戶端是由執行下列工作的程式檔案所組成：  
  
- 連接到 DB2 資料庫。  
  
- 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。  
  
- 將 DB2 資料庫物件轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]成語法。  
  
- 將物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]載入。  
  
- 將資料移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]至。  
  
本主題提供安裝 SSMA 的必要條件和指示。  
  
## <a name="prerequisites"></a>必要條件

SSMA 是設計用來搭配 db2 on z/OS 版本9.0 和10.0 或 db2 on LUW 版本9.8 和10.1 或更新版本， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以及2012或更新版本。  
  
安裝 SSMA 之前，請確定電腦符合下列需求：  
  
- Windows 7 或更新版本，或 Windows Server 2008 或更新版本。  
  
- [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 或更新版本。  
  
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] 4.0[!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)]版或更新版本。 4\.0 版可[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在產品媒體上取得。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 您也可以從[.NET Framework 開發人員中心](https://go.microsoft.com/fwlink/?LinkId=48882)取得。  
  
- Microsoft OLEDB Provider for DB2 第5版或更新版本，以及您要遷移之 DB2 資料庫的連線能力。  
  
- 在裝載目標實例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB 的電腦上存取和足夠的許可權，您將在其中遷移資料庫物件和資料。 如需詳細資訊，請參閱[連接&#40;到&#41;SQL Server DB2eToSQL](../../ssma/db2/connecting-to-sql-server-db2etosql.md)。  
  
- 建議使用 4 GB 的 RAM。  
  
## <a name="microsoft-oledb-provider-for-db2"></a>Microsoft OLEDB Provider for DB2  

若要下載 OLEDB provider for DB2 6.0 版，請移至[Microsoft® SQL Server® 2017 Feature Pack](https://www.microsoft.com/download/details.aspx?id=55992)。

SSMA 是 Web 下載。 若要下載最新版本，請參閱[SQL Server 移轉小幫手下載頁面](https://aka.ms/ssmafordb2)。  
  
下載最新版本之後，請將安裝檔案解壓縮，以便安裝 SSMA。  
  
若要安裝 SSMA 用戶端：
  
1. 按兩下 [SSMA for DB2 *n*]。安裝 .exe，其中*n*是組建編號。  
  
2. 在 [**歡迎使用**] 頁面上，選取 **[下一步]** 。  
  
   如果您沒有安裝必要條件，則會出現一則訊息，指出您必須先安裝必要的元件。 請確定您已安裝所有必要條件，然後再次執行安裝程式。  
  
3. 閱讀使用者授權合約。 如果您同意，請選取 **[我接受授權合約中的條款**]，然後選取 **[下一步]** 。  
  
4. 在 [**選擇安裝類型**] 頁面上，選取 [**一般**]。  
  
5. 選取 [安裝]。  
  
> [!IMPORTANT]  
> 請先卸載所有舊版的 SSMA for DB2，再安裝新版本。
  
預設安裝位置為 DB2 的 C:\Program Files\Microsoft SQL Server 移轉小幫手。  
  
## <a name="see-also"></a>另請參閱

[在 SQL Server &#40;DB2ToSQL 上安裝 SSMA 元件&#41;](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
[將 DB2 資料庫移轉至&#40;SQL Server DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
