---
title: 安裝 SQL Server 移轉小幫手以進行存取（AccessToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- installing SSMA
- instructions, installation
- instructions, upgrade
- licensing SSMA
- prerequisites for installing SSMA
- procedure, installation
- procedure, licensing
- procedure, upgrading
- removing SSMA
- Setup
- uninstalling SSMA
- upgrading SSMA
ms.assetid: dd50eebd-75df-4e0d-8c4d-88b511aae4c7
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 80fc19b17ac1c01f0c57d828a3bc4821050f761d
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257895"
---
# <a name="installing-sql-server-migration-assistant-for-access-accesstosql"></a>安裝 SQL Server 移轉小幫手以進行存取（AccessToSQL）
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]移轉小幫手（SSMA） for Access 是使用以 Windows Installer 為基礎的 wizard 來安裝。 本主題提供安裝必要條件的相關資訊、SSMA 最新版本的連結，以及安裝、授權、卸載和升級 SSMA 的指示。  
  
## <a name="prerequisites"></a>必要條件  
安裝 SSMA 之前，請確定您的系統符合下列需求：  
  
-   Windows 7 或更新版本，或 Windows Server 2008 或更新版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 或更新版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] .NET Framework 版本4.0 或更新版本。 .NET Framework 版本4.0 適用于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]產品光碟，並使用[Microsoft .net 指南](https://docs.microsoft.com/dotnet/framework/)中的資訊。
  
-   在裝載[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure DB 目標實例的電腦上存取和足夠的許可權，您將會在其中遷移資料庫物件和資料。  
  
-   Microsoft Data Access Object （DAO）提供者版本12.0 或14.0。 您可以從 Microsoft Office 2010/2007 產品安裝 DAO 提供者，或從 Microsoft 網站下載。  
  
-   適用于遷移至 SQL Azure 的 SQL Server Native Access 用戶端（SNAC）10.5 版和更新版本。 您可以從[Microsoft® SQL Server® 2008 R2 功能套件](https://www.microsoft.com/download/details.aspx?id=16978)取得最新版本的 SNAC  
  
-   4 GB RAM （建議選項）。  
  
## <a name="installing-ssma"></a>安裝 SSMA  
SSMA 是 Web 下載項目。 若要下載最新版本，請參閱[SQL Server 移轉小幫手下載頁面](https://aka.ms/ssmaforaccess)。  
  
下載最新版本之後，您必須先從解壓縮安裝檔案，才能安裝 SSMA。

> [!IMPORTANT]  
> -   安裝新版本之前，請先卸載所有先前版本的 SSMA 以進行存取。  
  
**若要安裝 SSMA**  
  
1.  按兩下 [SSMA] 以存取 [ *n*]，其中*n*是組建編號。  
  
2.  在 [歡迎] 頁面中按 [下一步] ****。  
  
    如果您未安裝必要條件，則會出現一則訊息，指出您必須先安裝必要的元件。 請確定您已安裝所有必要條件，然後再次執行安裝程式。  
  
3.  閱讀使用者授權合約;如果您同意，請選取 **[我接受合約**]，然後按 **[下一步]**。  
  
4.  在 [選擇安裝類型] 頁面上，按一下 [**一般**]。  
  
5.  按一下 **[安裝]**。  
  
預設安裝位置是 C:\Program Files\Microsoft SQL Server 移轉小幫手以進行存取。  
  
## <a name="uninstalling-ssma-for-access"></a>卸載 SSMA 以進行存取  
使用 [控制台] 中的 [**新增或移除程式**] 來卸載 SSMA。 請注意，卸載程式並不會刪除 SSMA 專案檔案或記錄檔。  
  
**卸載 SSMA**  
  
1.  按一下 [開始]****、[控制台]****，然後按一下 [新增或移除程式]****。  
  
2.  選取 [ **Microsoft SQL Server 移轉小幫手以進行存取**]，然後按一下 [**移除**]。  
  
## <a name="upgrading-to-a-later-version"></a>升級至更新版本  
如果您想要升級至較新版本的 SSMA 以進行存取，您必須先卸載 SSMA 才能存取，然後再安裝較新的版本。 遵循卸載 SSMA for Access 一節中的指示，完成此程式。  
  
如果您開啟在舊版 SSMA 中建立的專案以進行存取，SSMA 會詢問您是否要將專案轉換為較新的版本。 按一下 [**是]** 以在較新版本的 SSMA 中使用專案。  
  
## <a name="see-also"></a>另請參閱  
[準備 Access 資料庫以進行遷移](preparing-access-databases-for-migration-accesstosql.md)  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[將存取應用程式連結至 SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)  
  
