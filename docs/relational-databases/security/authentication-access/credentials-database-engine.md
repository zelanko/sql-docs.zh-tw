---
title: "認證 (Database Engine) | Microsoft Docs"
ms.custom: 
ms.date: 02/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- principals [SQL Server], credentials
- schemas [SQL Server], credentials
- permissions [SQL Server], credentials
- groups [SQL Server], credentials
- ALTER ANY CREDENTIAL permission
- security [SQL Server], credentials
- authentication [SQL Server], credentials
- users [SQL Server], credentials
- credentials [SQL Server], about credentials
- credentials [SQL Server]
ms.assetid: c8df6022-e0b4-46b8-9670-3f86938d3177
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ad9fe32b0bf2bed4908e7268ad85aae474e9e4cc
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="credentials-database-engine"></a>認證 (Database Engine)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  認證是包含驗證資訊 (認證) 的記錄，該項資訊是連接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]外部資源時所需的資訊， 此資訊會由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]用於內部。 大部份認證都包含 Windows 使用者名稱和密碼。  
  
 儲存在認證中的資訊可讓透過 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證連接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的使用者，可以存取在伺服器執行個體外部的資源。 如果外部資源為 Windows，則使用者會驗證為認證中指定的 Windows 使用者。 單一認證可對應至多個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入。 但是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入只能對應至一個認證。  
  
 如需儲存在 master 資料庫並且可以在整個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體中使用的認證，請參閱 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)。 如需由特定資料庫使用且該資料庫可攜的認證的詳細資訊，請參閱 [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-scoped-credential-transact-sql.md)。  
  
 系統認證會自動建立並與特定端點關聯。 系統認證的名稱是以兩個雜湊符號 (##) 開頭。  
  
 如需認證的詳細資訊，請參閱 [sys.credentials](../../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md) 和 [sys.database_scoped_credentials](../../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md) 目錄檢視。  
  
## <a name="related-content"></a>相關內容  
 [建立認證](../../../relational-databases/security/authentication-access/create-a-credential.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)   
 [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-scoped-credential-transact-sql.md)  
 [保護 SQL Server 的安全](../../../relational-databases/security/securing-sql-server.md)  
  
  
