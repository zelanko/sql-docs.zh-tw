---
title: "連接到 SQL Server (AccessToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: ceb77a97-d6d5-4a92-90a6-342e97d12b54
caps.latest.revision: 3
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 45bb4e967a58651675ab2e4bf62d0e096c3cb645
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="connect-to-sql-server-accesstosql"></a>連接到 SQL Server (AccessToSQL)
使用**連接到 SQL Server**對話方塊連接到的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]您想要移轉到。 若要存取**連接到 SQL Server**對話方塊**檔案**功能表上，按一下 **連接到 SQL Server**。  
  
## <a name="options"></a>選項。  
**伺服器名稱**  
輸入或選取要連接到 SQL Server 執行個體。 根據預設，會顯示您連接到最近的執行個體。  
  
-   如果您要連接到本機電腦上的預設執行個體，您可以輸入  **localhost**或一個點 (**。**)。  
  
-   如果您要連接到另一部電腦上的預設執行個體，請輸入電腦的名稱。  
  
-   如果您要連接到另一部電腦上的具名執行個體中，輸入電腦名稱、 反斜線和執行個體名稱，例如*MyServer*\\*MyInstance*。  
  
**伺服器通訊埠**  
如果您的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]未設定為接受連接，使用預設通訊埠 (1433)，輸入連接埠號碼。 否則，這個值保留空白。  
  
**資料庫**  
指定要移轉的物件和資料的資料庫。 此選項時，無法提供重新連接至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
**驗證**  
選取用來連接到的驗證方法[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 若要使用目前的 Windows 帳戶，請選取 [Windows 驗證]。 若要指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]登入和密碼，選取[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]驗證。  
  
**使用者名稱**  
如果您使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]驗證，該執行個體輸入的登入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 如果您使用 Windows 驗證，此選項無法使用。  
  
**密碼**  
如果您使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]驗證、 登入輸入密碼，該執行個體上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 如果您使用 Windows 驗證，此選項無法使用。  
  
**加密連接**  
如果您想要安全地連線到 SQL Server，請檢查使用的加密連接**加密連接**核取方塊。  
  
**信任伺服器憑證**  
如果您想要使用此選項，選取**信任伺服器憑證**核取方塊。  
  
> [!NOTE]  
> 若要啟用**信任伺服器憑證**，「 加密 」 必須設為**True**。  
  

