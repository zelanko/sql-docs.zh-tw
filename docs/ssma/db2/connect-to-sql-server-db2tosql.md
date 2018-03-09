---
title: "連接到 SQL Server (DB2ToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-db2
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: bc14a072-8949-4ee0-a4b4-ada55fe8df5c
caps.latest.revision: "3"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 336ea367d6c8a54e263eebc9bbb68350ed9dcfa9
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="connect-to-sql-server-db2tosql"></a>連接到 SQL Server (DB2ToSQL)
使用**連接到 SQL Server**對話方塊連接到的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]您想要移轉到。 若要存取**連接到 SQL Server**對話方塊**檔案**功能表上，按一下 **連接到 SQL Server**。  
  
## <a name="options"></a>選項。  
**伺服器名稱**  
輸入或選取要連接到 SQL Server 執行個體。 根據預設，會顯示您連接到最近的執行個體。  
  
-   如果您要連接到本機電腦上的預設執行個體，您可以輸入  **localhost**或一個點 (**。**)。  
  
-   如果您要連接到另一部電腦上的預設執行個體，請輸入電腦的名稱。  
  
-   如果您要連接到另一部電腦上的具名執行個體中，輸入電腦名稱、 反斜線和執行個體名稱，例如*MyServer*\\*MyInstance*。  
  
**伺服器通訊埠**  
如果您的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]未設定為接受連接，使用預設通訊埠 (1433)，輸入連接埠號碼。 否則，這個值保留空白。  
  
**[資料庫備份]**  
指定要移轉的物件和資料的資料庫。 此選項時，無法提供重新連接至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
**驗證**  
選取用來連接到的驗證方法[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 若要使用目前的 Windows 帳戶，請選取 [Windows 驗證]。 若要指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]登入和密碼，選取[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]驗證。  
  
**User name**  
如果您使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]驗證，該執行個體輸入的登入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 如果您使用 Windows 驗證，此選項無法使用。  
  
**密碼**  
如果您使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]驗證、 登入輸入密碼，該執行個體上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 如果您使用 Windows 驗證，此選項無法使用。  
  
**加密連接**  
如果您想要安全地連線到 SQL Server，請檢查使用的加密連接**加密連接**核取方塊。  
  
**信任伺服器憑證**  
如果您想要使用此選項，選取**信任伺服器憑證**核取方塊。  
  
> [!NOTE]  
> 若要啟用**信任伺服器憑證**，「 加密 」 必須設為**True**。  
  
