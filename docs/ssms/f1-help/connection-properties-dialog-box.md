---
title: "連接屬性對話方塊 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.connectionproperties.f1
helpviewer_keywords:
- Connection Properties dialog box
ms.assetid: 6df812ad-4d80-4503-8a23-47719ce85624
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8e258a6b81a9061c08ba4df098afa4e67c74df3a
ms.lasthandoff: 04/11/2017

---
# <a name="connection-properties-dialog-box"></a>連接屬性對話方塊
使用此對話方塊來檢視目前的連接屬性。 當您在各個物件總管對話方塊中按一下 [檢視連接屬性]****，就會出現此對話方塊。 此頁面上顯示的屬性是唯讀的。  
  
若要變更屬性 (例如 [資料庫]****)，請在開啟 [連接屬性]**** 對話方塊之前，先使用物件總管連接到想要的資料庫。  
  
請注意，SQL Azure 的查詢逾時期限是 30 分鐘。  
  
## <a name="authentication"></a>驗證  
檢視目前連接的驗證屬性。 驗證屬性是建立連接時的登入和驗證方法。 若要變更驗證屬性，請從 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中斷連接，然後使用想要的連接選項，再次將物件總管連接到伺服器。  
  
**驗證方法**  
目前連接所使用的驗證方法。  
  
**使用者名稱**  
用於連接驗證之登入的使用者名稱。  
  
## <a name="connection-category"></a>連接類別目錄  
檢視目前連接的連接屬性。 在連接處理期間，大部份的連接屬性都已在 [連接到伺服器]**** 對話方塊的 [連接屬性]**** 索引標籤上選取。  
  
**資料庫**  
目前連接的資料庫名稱。 若要變更此設定，請使用 SQL 編輯器工具列。  
  
**SPID**  
伺服器指派給連接的系統處理序識別碼。 此連接的這項設定無法變更。  
  
**網路通訊協定**  
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 連接的網路通訊協定。 若要變更這項設定，請使用所要的連接屬性重新連接。  
  
**網路封包大小**  
與伺服器通訊時使用的封包大小。 若要變更這項設定，請使用所要的連接屬性重新連接。  
  
**連接逾時**  
連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 時，在逾時並傳回連接失敗的錯誤訊息給使用者之前，要等候時間量，以秒為單位。 若要變更這項設定，請使用所要的連接屬性重新連接。  
  
**執行逾時**  
伺服器上的工作執行完成之前，要等候的時間量，以秒為單位。 若要變更這項設定，請使用所要的連接屬性重新連接。  
  
**已加密**  
決定目前的連接是否加密。 若要變更這項設定，請使用所要的連接屬性重新連接。  
  
## <a name="product-category"></a>Product Category  
檢視目前連接的產品屬性。 這些屬性會描述伺服器產品、版本、執行個體名稱和定序。 這些屬性會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 安裝時設定。  
  
**產品名稱**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 產品名稱。  
  
**產品版本**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 產品版本。  
  
**伺服器名稱**  
正在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]的電腦名稱。  
  
**執行個體名稱**  
伺服器的執行個體名稱。 預設的執行個體為空白。  
  
**語言**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 產品的語言版本。  
  
**定序**  
伺服器的定序。  
  
## <a name="server-environment-category"></a>伺服器環境類別目錄  
針對目前的連接，檢視與伺服器硬體和作業系統相關的伺服器環境屬性。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]無法設定這些屬性。  
  
**電腦名稱**  
正在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]的伺服器電腦名稱。  
  
**平台**  
伺服器的作業系統名稱、製造商名稱及 CPU 家族。  
  
**作業系統**  
伺服器上安裝的 [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows 版本。  
  
**處理器**  
伺服器上的處理器數目。  
  
**作業系統記憶體**  
伺服器上實體記憶體的總數 (以 MB 表示)。  
  
## <a name="see-also"></a>另請參閱  
[SQL Server Management Studio 中的屬性頁](../../ssms/property-pages-in-sql-server-management-studio.md)  
[連接到伺服器 &amp;#40;登入頁面&amp;#41; Database Engine](../../ssms/f1-help/connect-to-server-login-page-database-engine.md)  
  

