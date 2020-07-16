---
title: 安裝適用于 SAP ASE 用戶端的 SSMA （SybaseToSQL） |Microsoft Docs
description: 瞭解適用于 SAP 調適型伺服器 Enterprise （ASE）的 SQL Server 移轉小幫手（SSMA）安裝必要條件，以及如何安裝。
ms.custom: ''
ms.date: 07/14/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: e770c2f2-52b9-4471-a207-0d35df41399c
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 288b6458fc8429077472ba3ba7ad49e6d6fd7565
ms.sourcegitcommit: fd7b268a34562d70d46441f689543ecce7df2e4d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/16/2020
ms.locfileid: "86411166"
---
# <a name="installing-ssma-for-sap-ase-client-sybasetosql"></a>安裝適用于 SAP ASE 用戶端的 SSMA （SybaseToSQL）

SSMA 用戶端是由用來連接到 SAP 調適型伺服器 Enterprise （ASE）資料庫伺服器和實例的程式檔案 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ，將 ASE 資料庫物件轉換成或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 語法，將物件載入或，然後將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 資料移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 。

本主題提供安裝 SSMA 的必要條件和指示。

## <a name="prerequisites"></a>必要條件

SSMA 是設計用來與 SAP ASE 11.9.2 或更新版本，以及所有版本的搭配使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。

安裝 SSMA 之前，請確定電腦符合下列需求：

- Windows 7 或更新版本，或 Windows Server 2008 或更新版本。
- [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 或更新版本。
- [!INCLUDE[msCoName](../../includes/msconame_md.md)].NET Framework 版本4.7.2 或更新版本。 您可以從[.NET Framework 開發人員中心](https://go.microsoft.com/fwlink/?LinkId=48882)取得此檔案。
- Sybase OLE DB/ADO.Net/ODBC 提供者，以及包含您想要遷移之資料庫的 SAP ASE 資料庫伺服器的連線能力。 您可以從 SAP ASE 產品媒體安裝提供者。 如需連線的詳細資訊，請參閱[連接到 SYBASE ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)。
- 在裝載目標實例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 您要遷移資料庫物件和資料的電腦上，存取和足夠的許可權。 如需詳細資訊，請參閱連接到[SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md) / [連接到 Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)。
- 建議使用 4 GB 的 RAM。

## <a name="installing-the-ssma-for-sybase-client"></a>安裝適用于 Sybase 用戶端的 SSMA

SSMA 是 Web 下載項目。 若要下載最新版本，請參閱[SQL Server 移轉小幫手下載頁面](https://aka.ms/ssmaforsybase)。

若要安裝 SSMA 用戶端：

1. 按兩下 [ **SSMAforSybase_*n*.msi**]，其中*n*是組建編號。
2. 在 [歡迎使用] 頁面上，按 **[下一步]**。

   如果您未安裝必要條件，則會出現一則訊息，指出您必須先安裝必要的元件。 請確定您已安裝所有必要條件，然後再次執行安裝程式。

3. 閱讀使用者授權合約。 如果您同意，請選取 **[我接受合約**]，然後按 **[下一步]**。
4. 在 [選擇安裝類型] 頁面上，按一下 [**一般**]。
5. 在 [**準備安裝**] 頁面上，您可以啟用或停用每次工具啟動時的遙測和自動更新檢查。 按一下 [安裝]**** 可開始進行安裝。

> [!IMPORTANT]
> 請先卸載所有先前版本的 SSMA for Sybase，再安裝新版本。

預設安裝位置是 `C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase`。

除了 SSMA 程式檔案之外，您還必須在上安裝適用于 Sybase 擴充功能套件的 SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如需詳細資訊，請參閱[在 SQL Server &#40;SybaseToSQL&#41;上安裝 SSMA 元件](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)。

## <a name="see-also"></a>另請參閱

- [在 SQL Server 上安裝 SSMA 元件](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
- [將 Sybase ASE 資料庫移轉至 SQL Server-Azure SQL DB](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)
