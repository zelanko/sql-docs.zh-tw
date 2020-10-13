---
title: 保護 SQL Server 智慧財產權 | Microsoft Docs
description: 了解在散發給客戶的 SQL Server 資料應用程式中，用來保護智慧財產權的選項。
ms.custom: ''
ms.date: 01/31/2017
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- protecting intellectual property
- intellectual property
ms.assetid: 174a646a-d65c-4074-8249-d783e91be2dd
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 4619b4bd72258e67388ee7498eff63b28a1f3b03
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91869018"
---
# <a name="protecting-your-sql-server-intellectual-property"></a>保護 SQL Server 智慧財產權
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

軟體開發人員通常會問，要如何將其 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 資料應用程式散發給客戶，同時防止客戶分析和解構其應用程式。 這裡的重要原則在於保護智慧財產權、本身為法律問題，而且透過授權合約進行保護。 在其他人所管理的電腦上安裝 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 時，原本就會遺失一些控制權。 

## <a name="nature-of-the-problem"></a>問題本質
電腦的擁有者/系統管理員一律可以存取該電腦上安裝的 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 執行個體。 如果您將應用程式部署到客戶的電腦，因為他們是系統管理員，所以可以使用 **sysadmin** 固定伺服器角色成員的身分連線到 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 這包括可以授與權限、管理備份 (包括將備份還原到其他電腦)、解密以及移動資料檔案等等。如需詳細資訊，請參閱 [當系統管理員遭到鎖定時連接到 SQL Server](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md)。 

預存程序和資料可以進行加密，但無法隱藏資料結構，而且將偵錯工具附加至伺服器處理序的使用者可以在執行階段從記憶體中擷取已解密的程序和資料。

如果用戶端不是電腦上的系統管理員，則您可以防止用戶端進行存取。 您可以使用[透明資料加密](../../relational-databases/security/encryption/transparent-data-encryption.md)來加密資料檔案、加密備份，以及稽核所有使用者的動作。 但 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 系統管理員以及 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 電腦的系統管理員可以反轉這些動作。

## <a name="solution"></a>解決方法
不需要在用戶端電腦上安裝 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 就有各種方式可以設定用戶端資料存取。 最簡單的方法可能是使用 [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)]，但用戶端不是系統管理員，因此可以使用[永遠加密](../../relational-databases/security/encryption/always-encrypted-database-engine.md)。 如需 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 入門的詳細資訊，請參閱[什麼是 SQL Database？SQL Database 簡介](/azure/sql-database/sql-database-technical-overview)。  

您也可以在自己的網路上裝載 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，並允許用戶端直接或透過 Web 應用程式在網路上存取資料。

## <a name="see-also"></a>另請參閱

[SQL Server Database Engine 和 Azure SQL Database 的資訊安全中心](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
[保護 SQL Server 的安全](../../relational-databases/security/securing-sql-server.md)