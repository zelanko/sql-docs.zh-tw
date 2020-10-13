---
title: 安裝 SQL Server 移轉小幫手以存取 (AccessToSQL) |Microsoft Docs
description: 瞭解 SQL Server 移轉小幫手 (SSMA) 的安裝必要條件，以及如何安裝、授權、升級和卸載。
ms.prod: sql
ms.custom: ''
ms.date: 07/14/2020
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
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 1313699a3d82e0dbced8469f251a0a105f296246
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "91985214"
---
# <a name="installing-sql-server-migration-assistant-for-access-accesstosql"></a>安裝 SQL Server 移轉小幫手以存取 (AccessToSQL) 

[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Migration Assistant (SSMA) 可使用以 Windows Installer 為基礎的 wizard 安裝存取。 本主題提供安裝必要條件的相關資訊、最新版 SSMA 的連結，以及安裝、授權、卸載和升級 SSMA 的指示。

## <a name="prerequisites"></a>必要條件

在安裝 SSMA 之前，請確定您的系統符合下列需求：

- Windows 7 或更新版本，或 Windows Server 2008 或更新版本。
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 或更新版本。
- [!INCLUDE[msCoName](../../includes/msconame_md.md)].NET Framework 版本4.7.2 或更新版本。 您可以從 [Microsoft .Net 指南](/dotnet/framework/)取得 .NET Framework。
- 在裝載目標實例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 您要遷移資料庫物件和資料的電腦上，存取和擁有足夠的許可權。
- Microsoft Data Access 物件 (DAO) 提供者版本12.0 或14.0。 您可以從 Microsoft Office 2010/2007 產品安裝 DAO 提供者，或從 Microsoft 網站下載。
- 4 GB 的 RAM (建議的) 。

## <a name="installing-ssma"></a>安裝 SSMA

SSMA 是 Web 下載項目。 若要下載最新版本，請參閱 [SQL Server 移轉小幫手下載頁面](https://aka.ms/ssmaforaccess)。

> [!IMPORTANT]
> 在安裝新版本之前，請先卸載所有先前版本的 SSMA 以進行存取。

若要安裝 SSMA：
  
1. 按兩下 **SSMAforAccess_*n*.msi**，其中 *n* 是組建編號。
2. 在 [歡迎使用] 頁面上，按 **[下一步]**。

   如果您未安裝必要條件，則會出現一則訊息，指出您必須先安裝必要的元件。 請確定您已安裝所有必要條件，然後再次執行安裝程式。

3. 閱讀 End-User 授權合約;如果您同意，請選取 **[我接受合約**]，然後按 **[下一步]**。
4. 在 [ **選擇安裝類型** ] 頁面上，按一下 [ **一般**]。
5. 在 [ **準備安裝** ] 頁面上，您可以在每次工具啟動時啟用或停用遙測和自動更新檢查。 按一下 [安裝]**** 可開始進行安裝。
  
預設安裝位置是 `C:\Program Files\Microsoft SQL Server Migration Assistant for Access`。

## <a name="uninstalling-ssma-for-access"></a>正在卸載 SSMA 以進行存取

使用主控台中的 [ **新增或移除程式** ] 卸載 SSMA。 請注意，卸載程式並不會刪除 SSMA 專案檔案或記錄檔。

卸載 SSMA：

1. 按一下 [開始]****、[控制台]****，然後按一下 [新增或移除程式]****。
2. 選取 [ **存取 Microsoft SQL Server 移轉小幫手**]，然後按一下 [ **移除**]。

## <a name="upgrading-to-a-later-version"></a>升級至較新版本

如果您想要升級至較新版本的 SSMA 進行存取，您必須先卸載 SSMA 以進行存取，然後再安裝較新的版本。 請依照 < 卸載 SSMA for Access 一節中的指示操作，以完成此程式。

如果您開啟以舊版 SSMA 所建立的專案以供存取，SSMA 可能會詢問您是否要將專案轉換為較新的版本。 按一下 [ **是]** 可在較新版本的 SSMA 中使用專案。

## <a name="see-also"></a>另請參閱

- [準備 Access 資料庫以進行遷移](preparing-access-databases-for-migration-accesstosql.md)
- [將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)
- [將 Access 應用程式連結至 SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)