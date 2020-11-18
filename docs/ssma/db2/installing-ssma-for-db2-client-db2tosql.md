---
title: 安裝 SSMA for DB2 用戶端 (DB2ToSQL) |Microsoft Docs
description: 瞭解 SQL Server 移轉小幫手 (SSMA) for DB2 用戶端的安裝必要條件和安裝方式。
ms.prod: sql
ms.custom: ''
ms.date: 07/14/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 3ae2a470-6afd-4512-b6d1-fcbe6afe88ad
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: a223f5dbf6e100ac776e2f3aebad51c9bb885abf
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94869596"
---
# <a name="installing-ssma-for-db2-client-db2tosql"></a>安裝 SSMA for DB2 用戶端 (DB2ToSQL) 

SSMA 用戶端是由執行下列工作的程式檔所組成：

- 連接到 DB2 資料庫。
- 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。
- 將 DB2 資料庫物件轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 語法。
- 將物件載入至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。
- 將資料移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。

本主題提供安裝 SSMA 的安裝必要條件和指示。

## <a name="prerequisites"></a>先決條件

SSMA 的設計目的是使用 DB2 on z/OS 版本9.0 和10.0、DB2 on LUW 9.8 和10.1 或更新版本、DB2 for i 版本7.1 或更高、更高的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 或更新版本。

在安裝 SSMA 之前，請確定電腦符合下列需求：

- Windows 7 或更新版本，或 Windows Server 2008 或更新版本。
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 或更新版本。
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 版本4.7.2 或更新版本。 您可以從 [.NET Framework 開發人員中心](https://go.microsoft.com/fwlink/?LinkId=48882)取得。
- Microsoft OLE DB Provider for DB2 第5版或更新版本，以及您想要遷移之 DB2 資料庫的連線能力。
- 存取裝載目標實例之電腦上的和足夠的許可權， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database 您將在其中遷移資料庫物件和資料的許可權。 如需詳細資訊，請參閱 [連接到 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/connecting-to-sql-server-db2tosql.md)。
- 建議 4 GB 的 RAM。

## <a name="microsoft-ole-db-provider-for-db2"></a>Microsoft OLE DB Provider for DB2

若要下載 OLE DB provider for DB2 6.0 版，請移至 [Microsoft® SQL Server® 2017 Feature Pack](https://www.microsoft.com/download/details.aspx?id=55992)。

SSMA 是 Web 下載項目。 若要下載最新版本，請參閱 [SQL Server 移轉小幫手下載頁面](https://aka.ms/ssmafordb2)。

若要安裝 SSMA 用戶端：

1. 按兩下 **SSMAforDB2_ *n*.msi**，其中 *n* 是組建編號。
2. 在 [歡迎]  頁面上，選取 [下一步]  。

   如果您未安裝必要條件，則會出現一則訊息，指出您必須先安裝必要的元件。 請確定您已安裝所有必要條件，然後再次執行安裝程式。

3. 閱讀 End-User 授權合約。 如果您同意，請選取 **[我接受合約**]，然後選取 **[下一步]**。
4. 在 [ **選擇安裝類型** ] 頁面上，選取 [ **一般**]。
5. 在 [ **準備安裝** ] 頁面上，您可以在每次工具啟動時啟用或停用遙測和自動更新檢查。 按一下 [安裝] 可開始進行安裝。

> [!IMPORTANT]
> 請先卸載所有先前版本的 SSMA for DB2，再安裝新版本。

預設安裝位置是 `C:\Program Files\Microsoft SQL Server Migration Assistant for DB2`。

## <a name="see-also"></a>請參閱

- [在 SQL Server 上安裝 SSMA 元件](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)
- [將 DB2 資料庫移轉到 SQL Server](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)
