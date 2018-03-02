---
title: "Active Directory 驗證 Linux 上的 SQL Server |Microsoft 文件"
description: "本文章提供在 Linux 上的 SQL server 的 Active Directory 驗證的概觀。"
author: rothja
ms.date: 02/23/2018
ms.author: jroth
manager: craigg
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
helpviewer_keywords:
- Linux, AAD authentication
ms.workload: On Demand
ms.openlocfilehash: f3c516465d9703ae736350e660aefba15a5636c9
ms.sourcegitcommit: f0c5e37c138be5fb2cbb93e9f2ded307665b54ea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/24/2018
---
# <a name="active-directory-authentication-for-sql-server-on-linux"></a>Active Directory 驗證的 SQL Server on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文提供的 Active Directory (AD) 驗證概觀[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]on Linux。 AD 驗證就是所謂的整合式的驗證[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 

## <a name="ad-authentication-overview"></a>AD 驗證概觀

AD 驗證可讓已加入網域的用戶端的 Windows 或 Linux 向[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用其網域認證和 Kerberos 通訊協定。

AD 驗證透過具有下列優點[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]驗證：

- 使用者驗證透過單一登入，而不會提示輸入密碼。   
- 藉由建立的 AD 群組的登入，您可以管理存取權與權限[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用 AD 群組成員資格。  
- 每位使用者都有單一識別您的組織，因此您不需要追蹤其中的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]登入對應至哪些使用者。   
- AD 可讓您強制執行組織的集中式的密碼原則。   

## <a name="configuration-steps"></a>組態步驟

若要使用 Active Directory 驗證，您必須有的 AD 網域控制站 (Windows) 網路上。

教學課程中，提供如何設定 AD 驗證的詳細資料[教學課程： 使用 Active Directory 驗證與 SQL Server on Linux](sql-server-linux-active-directory-authentication.md)。 下列清單提供教學課程中的摘要，包含每個區段的連結：

1. [加入 Active Directory 網域的 SQL Server 主機](sql-server-linux-active-directory-authentication.md#join)。
1. [適用於 SQL Server 中建立 AD 使用者，並設定 ServicePrincipalName](sql-server-linux-active-directory-authentication.md#createuser)。
1. [設定 SQL Server 服務 keytab](sql-server-linux-active-directory-authentication.md#configurekeytab)。
1. [在 TRANSACT-SQL 中建立 AD 為基礎的 SQL Server 登入](sql-server-linux-active-directory-authentication.md#createsqllogins)。
1. [連接到 SQL Server 使用 AD 驗證](sql-server-linux-active-directory-authentication.md#connect)。

## <a name="known-issues"></a>已知問題

- 此時，資料庫鏡像端點支援的唯一的驗證方法是憑證。 在未來版本中，將會啟用 WINDOWS 驗證方法。
- 第三方 AD 工具 Centrify，Powerbroker，等 Vintela 不支援。

## <a name="next-steps"></a>後續步驟

如需有關如何在 Linux 上實作適用於 SQL Server 的 Active Directory 驗證的詳細資訊，請參閱[教學課程： 使用 Active Directory 驗證與 SQL Server on Linux](sql-server-linux-active-directory-authentication.md)。