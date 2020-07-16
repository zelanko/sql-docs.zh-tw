---
title: 安裝 SSMA for Oracle 用戶端（OracleToSQL） |Microsoft Docs
description: 瞭解適用于 Oracle 用戶端的 SQL Server 移轉小幫手（SSMA）安裝必要條件，以及如何安裝。
ms.prod: sql
ms.custom: ''
ms.date: 07/14/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: d5d4903d-e296-4bbf-8780-63674c4d62d5
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 939504092ef7ae9dc13bdcf829f6ea5e88ce59f9
ms.sourcegitcommit: fd7b268a34562d70d46441f689543ecce7df2e4d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/16/2020
ms.locfileid: "86411266"
---
# <a name="installing-ssma-for-oracle-client-oracletosql"></a>安裝 SSMA for Oracle 用戶端（OracleToSQL）

SSMA 用戶端是由執行下列工作的程式檔案所組成：  
  
- 連接到 Oracle 資料庫。
- 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。
- 將 Oracle 資料庫物件轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 語法。
- 將物件載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。
- 將資料移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。

本主題提供安裝 SSMA 的必要條件和指示。

## <a name="prerequisites"></a>必要條件

SSMA 是設計用來搭配 Oracle 9 或更新版本，以及的所有版本 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。

安裝 SSMA 之前，請確定電腦符合下列需求：

- Windows 7 或更新版本，或 Windows Server 2008 或更新版本。
- [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 或更新版本。
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 版本4.7.2 或更新版本。 您可以從[.NET Framework 開發人員中心](https://go.microsoft.com/fwlink/?LinkId=48882)取得此檔案。
- 連接到您想要遷移的 Oracle 資料庫。
- 在裝載目標實例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 您要遷移資料庫物件和資料的電腦上，存取和足夠的許可權。 如需詳細資訊，請參閱[連接到 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)。
- 建議使用 4 GB 的 RAM。  
  
## <a name="installing-the-ssma-for-oracle-client"></a>安裝 SSMA for Oracle 用戶端

SSMA 是 Web 下載項目。 若要下載最新版本，請參閱[SQL Server 移轉小幫手下載頁面](https://aka.ms/ssmafororacle)。

若要安裝 SSMA 用戶端：

1. 按兩下 [ **SSMAforOracle_*n*.msi**]，其中*n*是組建編號。
2. 在 [歡迎使用] 頁面上，按 **[下一步]**。

   如果您未安裝必要條件，則會出現一則訊息，指出您必須先安裝必要的元件。 請確定您已安裝所有必要條件，然後再次執行安裝程式。  

3. 閱讀使用者授權合約。 如果您同意，請選取 **[我接受合約**]，然後按 **[下一步]**。
4. 在 [**選擇安裝類型**] 頁面上，按一下 [**一般**]。
5. 在 [**準備安裝**] 頁面上，您可以啟用或停用每次工具啟動時的遙測和自動更新檢查。 按一下 [安裝]**** 可開始進行安裝。

> [!IMPORTANT]
> 請先卸載所有舊版的 SSMA for Oracle，再安裝新版本。

預設安裝位置是 `C:\Program Files\Microsoft SQL Server Migration Assistant for Oracle`。

除了 SSMA 程式檔案之外，您還必須在上安裝 SSMA for Oracle Extension Pack [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如需詳細資訊，請參閱[在 SQL Server 上安裝 SSMA 元件](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)。

## <a name="see-also"></a>另請參閱

- [在 SQL Server 上安裝 SSMA 元件](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)
- [將 Oracle 資料庫移轉到 SQL Server](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)
