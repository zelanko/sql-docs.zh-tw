---
title: 適用於 Linux 上 SQL Server 的 Active Directory 驗證
titleSuffix: SQL Server
description: 本文提供適用於 Linux 上 SQL Server 的 Active Directory 驗證概觀。
ms.date: 04/01/2019
author: Dylan-MSFT
ms.author: dygray
ms.reviewer: vanto
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
helpviewer_keywords:
- Linux, AAD authentication
ms.openlocfilehash: 32ff23fe1ea7f0a892a19cc6be0eef8439ee907f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "75831820"
---
# <a name="active-directory-authentication-for-sql-server-on-linux"></a>適用於 Linux 上 SQL Server 的 Active Directory 驗證

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文提供適用於 Linux 上 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的 Active Directory (AD) 驗證概觀。 AD 驗證在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 又稱為整合式驗證。

## <a name="ad-authentication-overview"></a>AD 驗證概觀

AD 驗證可讓 Windows 或 Linux 上加入網域的用戶端，使用其網域認證和 Kerberos 通訊協定向 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 進行驗證。

AD 驗證與 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證相較下具有下列優點：

- 使用者會透過單一登入進行驗證，而不是在出現輸入密碼的提示下進行驗證。
- 藉由建立 AD 群組的登入，您就能夠以 AD 群組成員資格，管理 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的存取和權限。  
- 每位使用者在整個組織內只有一個身分識別，因此您不需要追蹤哪個 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 登入對應到哪個人員。   
- AD 可讓您在整個組織內實行集中式密碼原則。

## <a name="configuration-steps"></a>組態步驟

若要使用 Active Directory 驗證，您的網路上必須有 AD 網域控制站 (Windows)。

如需如何設定 AD 驗證的詳細資訊，請參閱[教學課程：在 Linux 上的 SQL Server 使用 Active Directory 驗證](sql-server-linux-active-directory-authentication.md)。 下列清單提供連結至教學課程中每一節的摘要：

1. [將 SQL Server 主機加入 Active Directory 網域](sql-server-linux-active-directory-join-domain.md)。
1. [建立 SQL Server 的 AD 使用者並設定 ServicePrincipalName](sql-server-linux-active-directory-authentication.md#createuser)。
1. [設定 SQL Server 服務 Keytab](sql-server-linux-active-directory-authentication.md#configurekeytab)。
1. [保護 Keytab 檔案](sql-server-linux-active-directory-authentication.md#configurekeytab)。
1. [設定 SQL Server 以使用 Keytab 檔案進行 Kerberos 驗證](sql-server-linux-active-directory-authentication.md#configurekeytab)。
1. [在 Transact-SQL 中建立以 AD 為基礎的 SQL Server 登入](sql-server-linux-active-directory-authentication.md#createsqllogins)。
1. [使用 AD 驗證連線到 SQL Server](sql-server-linux-active-directory-authentication.md#connect)。

## <a name="known-issues"></a>已知問題

- 目前，資料庫鏡像端點唯一支援的驗證方法是 CERTIFICATE。 未來的版本將啟用 WINDOWS 驗證方法。

## <a name="next-steps"></a>後續步驟

如需如何對 Linux 上的 SQL Server 實作 Active Directory 驗證的詳細資訊，請參閱[教學課程：在 Linux 上的 SQL Server 使用 Active Directory 驗證](sql-server-linux-active-directory-authentication.md)。
