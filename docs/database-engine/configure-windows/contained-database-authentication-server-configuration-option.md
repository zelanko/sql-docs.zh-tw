---
title: 自主資料庫驗證伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- contained database, enabling
- contained database authentication option
ms.assetid: b80768d2-ac20-4035-a335-d9adb74b3f6e
caps.latest.revision: 11
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 57688eaacdfe7c4caaca489e4cac3df79823a51d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="contained-database-authentication-server-configuration-option"></a>自主資料庫驗證伺服器組態選項
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  使用  [自主資料庫驗證] 選項，可在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]執行個體上啟用自主資料庫。  
  
 此伺服器選項可讓您控制 **自主資料庫驗證**。  
  
-   當執行個體的  [自主資料庫驗證] 為關 (0) 時，自主資料庫便無法建立，或附加到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
-   當執行個體的  [自主資料庫驗證] 為開 (1) 時，自主資料庫就可以建立，或附加到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
 自主資料庫包含了定義資料庫所需的所有資料庫設定和中繼資料，而且對於已安裝資料庫的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體沒有組態相依性。 使用者可以連接至資料庫，而不需要在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 層級驗證登入。 將資料庫與 Database Engine 隔離，可讓您輕鬆地將資料庫移至另一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。 將所有資料庫設定包含在資料庫中，可讓資料庫擁有者管理該資料庫的所有組態設定。 如需自主資料庫的詳細資訊，請參閱 [自主資料庫](../../relational-databases/databases/contained-databases.md)。  

> [!NOTE]
> [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 和 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] 一律會啟用自主資料庫且無法停用。
  
 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體具有任何自主資料庫，您就可以使用 **RECONFIGURE WITH OVERRIDE** 陳述式，將 [自主資料庫驗證]  設定設為 0。 將 [自主資料庫驗證]  設為 0 將會停用自主資料庫的自主資料庫驗證。  
  
> [!IMPORTANT]  
>  當啟用自主的資料庫時，具有 ALTER ANY USER 權限 (例如 db_owner 和 db_accessadmin 資料庫角色) 的資料庫使用者可以存取資料庫，且可藉此來存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體。 這表示伺服器存取的控制權不再限於系統管理員和安全性管理員固定伺服器角色，且以具有 CONTROL SERVER和 ALTER ANY LOGIN 伺服器層級的權限來登入。 在允許自主資料庫之前，您應該了解自主資料庫的相關風險。 如需詳細資訊，請參閱 [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md)。  
  
## <a name="examples"></a>範例  
 下列範例會在 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體上啟用自主資料庫。  
  
```sql  
sp_configure 'contained database authentication', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
