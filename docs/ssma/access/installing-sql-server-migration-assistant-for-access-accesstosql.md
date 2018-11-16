---
title: 安裝 SQL Server Migration Assistant for Access (AccessToSQL) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 128c83e0fd63b2724311aec046bdb9683c569a03
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51664117"
---
# <a name="installing-sql-server-migration-assistant-for-access-accesstosql"></a>安裝 SQL Server Migration Assistant for Access (AccessToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 移轉小幫手 (SSMA) 的存取使用精靈來安裝 Windows Installer 為基礎。 本主題提供有關安裝必要條件的資訊 SSMA，最新版本的連結和安裝、 授權、 解除安裝和升級 SSMA 的指示。  
  
## <a name="prerequisites"></a>先決條件  
安裝 SSMA 之前，請確定您的系統符合下列需求：  
  
-   Windows 7 或更新版本，或 Windows Server 2008 或更新版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 或更新版本。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] .NET Framework 4.0 版或更新版本。 .NET Framework 4.0 版位於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]產品光碟片，以及使用中的資訊[Microsoft.NET 指南](https://docs.microsoft.com/dotnet/framework/)。
  
-   若要存取和裝載目標執行個體的電腦上有足夠的權限[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SQL Azure 資料庫移轉到這裡您將會是資料庫物件和資料。  
  
-   Microsoft 資料存取物件 (DAO) 提供者版本 12.0 或 14.0。 您可以從 Microsoft Office 2010/2007年產品安裝 DAO 提供者，或從 Microsoft 網站下載。  
  
-   SQL Server Native Access Client (SNAC) 版本為 10.5 和更新版本移轉至 SQL Azure。 您可以取得最新版的 SNAC 從[Microsoft® SQL Server® 2008 R2 功能套件](https://go.microsoft.com/fwlink/?LinkId=196940)  
  
-   4 GB 的 RAM （建議選項）。  
  
## <a name="installing-ssma"></a>安裝 SSMA  
SSMA 是 Web 下載項目。 若要下載最新版本，請參閱[SQL Server Migration Assistant 的下載頁面](https://aka.ms/ssmaforaccess)。  
  
下載最新版本之後，您必須先解壓縮安裝檔案，才能安裝 SSMA。

> [!IMPORTANT]  
> -   請安裝新版本之前，解除安裝所有舊版的 SSMA for Access。  
  
**安裝 SSMA**  
  
1.  按兩下 SSMA for Access *n*.msi，其中*n*是組建編號。  
  
2.  在 歡迎使用 頁面上，按一下**下一步**。  
  
    如果您沒有安裝必要條件，則會出現訊息，指出您必須先安裝必要的元件。 請確定您已安裝所有必要條件，然後再次執行安裝程式。  
  
3.  閱讀使用者授權合約 」;如果您同意，請選取**我接受合約**，然後按一下**下一步**。  
  
4.  在 [選擇安裝類型] 頁面上，按一下**典型**。  
  
5.  按一下 **[安裝]**。  
  
預設安裝位置是 C:\Program Files\Microsoft SQL Server Migration Assistant for Access。  
  
## <a name="uninstalling-ssma-for-access"></a>解除安裝 SSMA for Access  
使用解除安裝 SSMA**新增或移除程式**控制項台中。 請注意，解除安裝程式不會刪除 SSMA 專案檔或記錄檔。  
  
**若要解除安裝 SSMA**  
  
1.  按一下 **開始**，按一下**控制台**，然後按一下**新增或移除程式**。  
  
2.  選取  **Microsoft SQL Server Migration Assistant for Access**，然後按一下**移除**。  
  
## <a name="upgrading-to-a-later-version"></a>升級至較新版本  
如果您想要升級至更新版本的 SSMA for Access，您必須先解除安裝 SSMA for Access，然後再安裝較新的版本。 解除安裝的 SSMA 中遵循以完成此程序的 [存取] 區段。  
  
如果您開啟較早版本的 SSMA for Access 中建立的專案時，會要求 SSMA，如果您想要將專案轉換成較新版本。 按一下 **是**才能使用較新版本的 SSMA 中的專案。  
  
## <a name="see-also"></a>另請參閱  
[準備移轉的 Access 資料庫](preparing-access-databases-for-migration-accesstosql.md)  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[連結到 SQL Server 的 Access 應用程式](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)  
  
