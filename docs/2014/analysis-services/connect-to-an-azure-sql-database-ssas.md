---
title: 連接到 Azure SQL Database (SSAS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.connsqlazure.f1
ms.assetid: 4e0344e9-1822-4698-ad22-05f1f341ced7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9032249e880f11f27edd53e23d4ca54a47b920db
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66087144"
---
# <a name="connect-to-an-azure-sql-database-ssas"></a>連接到 Azure SQL 資料庫 (SSAS)
  [資料表匯入精靈] 的這個頁面可讓您連接到 [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)]。 若要從 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]存取精靈，請按一下 **[模型]** 功能表上的 **[從資料來源匯入]**。  
  
> [!NOTE]  
>  如果您要連接到 Azure DataMarket 資料集，請參閱[連接到報表或資料摘要 &#40;SSAS&#41;](connect-to-a-report-or-data-feed-ssas.md)。  
  
 [!INCLUDE[ssSDS](../includes/sssds-md.md)] 是裝載型的關聯式資料庫，您可以使用 SQL Server 驗證與其連接。 如需有關 [!INCLUDE[ssSDS](../includes/sssds-md.md)]的詳細資訊，請參閱 [SQL 資料庫](https://go.microsoft.com/fwlink/?LinkID=157856)網站。 若要連接至資料來源，您必須先在電腦上安裝適當的提供者。  
  
> [!NOTE]  
>  在這個頁面中選取資料庫時，會使用目前使用者的認證。 不過，如果在 [模擬資訊] 頁面中指定的使用者未具備從所選取資料庫讀取的權限，則匯入將不會成功。  
  
## <a name="uielement-list"></a>UIElement 清單  
 **易記連接名稱**  
 為此資料來源連接輸入唯一的名稱。 這是必要的欄位。  
  
 **伺服器名稱**  
 輸入要連接的伺服器名稱或 IP 位址。  
  
 **使用者名稱**  
 為資料庫連接指定使用者名稱。  
  
 這個使用者名稱是在建構資料來源的連接字串時使用。 這些認證也會在預覽和篩選 [資料表屬性] 視窗和 [匯入精靈] 中的資料時使用。 這些認證不會用來匯入或重新整理資料，而是會使用 [模擬資訊] 頁面上指定的 Windows 認證。  
  
 **密碼**  
 為資料庫連接指定密碼。  
  
 **儲存我的密碼**  
 指定是否要儲存您在 **[密碼]** 方塊中輸入的密碼。  
  
 **資料庫名稱**  
 從資料庫清單中選取資料庫。  
  
 **進階**  
 使用 **[設定進階屬性]** 對話方塊設定其他連接屬性。 如需詳細資訊，請參閱[設定進階屬性 &#40;SSAS&#41;](set-advanced-properties-ssas.md)。  
  
 **測試連接**  
 嘗試使用目前的設定建立與資料來源之間的連接。 顯示一則訊息，指出連接是否成功。  
  
  
