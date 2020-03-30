---
title: 連接到伺服器 (連接屬性頁面) Database Engine
ms.custom: seo-lt-2019
ms.date: 08/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.connecttoce.connectionproperties.f1
- sql13.swb.connecttosqlserver.connectionproperties.f1
ms.assetid: edc1143c-6a47-4b02-92ab-441bdea8ea8a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cb62bd419c08b1562a6b636685e360501f574ae3
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75245013"
---
# <a name="connect-to-server-connection-properties-page-database-engine"></a>連接到伺服器 (連接屬性頁面) Database Engine
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
當您連接到 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)] 執行個體或在 [已註冊的伺服器]  中註冊 [!INCLUDE[ssDE](../../includes/ssde_md.md)] 時，請使用這個索引標籤來檢視或指定選項。 連接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)] 執行個體時，[連接]  和 [選項]  才會出現在這個對話方塊中。 註冊 [!INCLUDE[ssDE](../../includes/ssde_md.md)] 時，[測試]  和 [儲存]  才會出現在這個對話方塊中。  
  
**連接到資料庫**  
從清單中選取要連接的資料庫。 如果您選取 **<default>** ，就會連線到伺服器的預設資料庫。 如果您選取 **<Browse server>** ，您就可以瀏覽伺服器來尋找您要連接的資料庫。  
  
當您透過 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Database Engine 執行個體時，您必須使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，並在 [連接到伺服器]  對話方塊的 [連接屬性]  索引標籤上指定資料庫。請務必選取 [加密連接]  核取方塊。  
  
根據預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會連接到 **master**。 連線到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 時，如果您指定使用者資料庫，就只會看到該資料庫及其在物件總管中的物件。 如果您連線到 **master**，您將能夠看到所有資料庫。 如需詳細資訊，請參閱 [Microsoft Azure SQL Database 概觀](/azure/sql-database/sql-database-technical-overview)。  
  
**網路通訊協定**  
從清單中選取通訊協定。 可用的用戶端通訊協定會使用 [電腦管理] 中的 [用戶端網路組態] 進行設定。  
  
**網路封包大小**  
輸入要傳送之網路封包的大小。 預設值是 4096 個位元組。  
  
**連接逾時**  
輸入在逾時之前所要等候建立連接的秒數。預設值為 15 秒。  
  
**執行逾時**  
輸入在伺服器上執行的工作完成之前，所要等候的時間 (以秒為單位)。 預設值為零秒，此值會指出沒有逾時。  
  
**加密連接**  
強制連接的加密。  
  
**使用自訂色彩**  
選取此選項可在 [!INCLUDE[ssDE](../../includes/ssde_md.md)] [查詢編輯器] 視窗中指定狀態列的背景色彩。 若要指定色彩，請按一下 [選取]  。 在 [色彩]  對話方塊中，從 [基本色彩]  方格選取預先定義的色彩，或是按一下 [定義自訂色彩]  來定義及使用自訂色彩。  
  
-   當您在 [物件總管]  窗格內指定伺服器項目的色彩時，該色彩會在開啟 [查詢編輯器] 視窗時使用。 若要開啟 [查詢編輯器] 視窗，請以滑鼠右鍵按一下伺服器項目並選取 [新增查詢]  ，或是在 [物件總管]  窗格為使用中而且在此伺服器上為焦點所在時，按一下工具列上的 [新增查詢]  。  
  
-   當您在 [已註冊的伺服器]  窗格內指定伺服器項目的色彩時，該色彩會在開啟 [查詢編輯器] 視窗時使用。 若要開啟 [查詢編輯器] 視窗，請以滑鼠右鍵按一下伺服器項目並選取 [新增查詢]  ，或是在 [已註冊的伺服器]  窗格為使用中而且在此伺服器上為焦點所在時，按一下工具列上的 [新增查詢]  。  
  
-   在 [檔案]  功能表上，當您按一下 [新增]  然後按一下 [Database Engine 查詢]  時，您在 [連接到伺服器]  對話方塊內指定的色彩會套用到 [查詢編輯器] 視窗。  
  
**AD 網域名稱或租用戶識別碼**  
使用 [Active Directory - 與 MFA 通用]  驗證來連線時，請指定驗證的網域。 此選項僅在使用 SSMS 17.2 版或更新版本時才可使用。 

**全部重設**  
將所有手動輸入的連接屬性值取代成預設值。  
  
**[連接]**  
使用列出的值嘗試進行連接。  
  
**選項**  
按一下即可變更對話方塊，並隱藏其他伺服器連接選項，例如記住密碼。  
  
**Test**  
在 [已註冊的伺服器]  中註冊 [!INCLUDE[ssDE](../../includes/ssde_md.md)] 時，請按一下以測試連接。  
  
**儲存**  
儲存 [已註冊的伺服器]  中的設定。  
  
## <a name="see-also"></a>另請參閱  
[連接屬性對話方塊](../../ssms/f1-help/connection-properties-dialog-box.md)  
  
