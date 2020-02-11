---
title: 連接到伺服器 (連接屬性頁面) 資料庫引擎 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.swb.connecttosqlserver.connectionproperties.f1
ms.assetid: edc1143c-6a47-4b02-92ab-441bdea8ea8a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 30382bcb0c70fb985c88866602cb997988b88569
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "70153756"
---
# <a name="connect-to-server-connection-properties-page-database-engine"></a>連接到伺服器 (連接屬性頁面) Database Engine
  當連接到的實例或在[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] **已註冊的伺服器**上註冊[!INCLUDE[ssDE](../../includes/ssde-md.md)]時，使用此索引標籤來查看或指定選項。 當連接到實例時， **[連接**] 和 [**選項**] 才會出現[!INCLUDE[ssDE](../../includes/ssde-md.md)]在這個對話方塊中。 註冊[!INCLUDE[ssDE](../../includes/ssde-md.md)]時，只會在此對話方塊中顯示 [**測試**] 和 [**儲存**]。  
  
## <a name="options"></a>選項。  
 **連線到資料庫**  
 從清單中選取要連接的資料庫。 如果您選取** \<[預設>**]，則會連接到伺服器的預設資料庫。 如果您選取** \<[流覽伺服器>**]，則可以流覽伺服器以取得要連接的資料庫。  
  
 透過[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫引擎的實例時，您必須使用驗證，並在 [連線**到伺服器**] 對話方塊的 [**連接屬性**] 索引標籤上指定資料庫。請確定您選取 [**加密連接**] 核取方塊。  
  
 根據預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會連接到 **master**。 如果您指定使用者資料庫，您只會在物件總管中看到該資料庫與其物件。 如果您連接到 **master**，您將能夠看到所有資料庫。 如需詳細資訊，請參閱[Azure SQL Database 總覽](/azure/sql-database/sql-database-technical-overview)。  
  
 **網路通訊協定**  
 從清單中選取通訊協定。 可用的用戶端通訊協定就是您在 [電腦管理] 中使用 [用戶端網路組態] 所設定的通訊協定。  
  
 **網路封包大小**  
 輸入要傳送之網路封包的大小。 預設值是 4096 個位元組。  
  
 **連接逾時**  
 輸入在超時之前，等候連線建立的秒數。預設值為15秒。  
  
 **執行超時**  
 輸入在伺服器上執行的工作完成之前，所要等候的時間 (以秒為單位)。 預設值為零秒，此值會指出沒有逾時。  
  
 **加密連接**  
 強制連接的加密。  
  
 **使用自訂色彩**  
 選取此選項可在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] [查詢編輯器] 視窗中指定狀態列的背景色彩。 若要指定色彩，請按一下 [選取]****。 在 [色彩]**** 對話方塊中，從 [基本色彩]**** 方格選取預先定義的色彩，或是按一下 [定義自訂色彩]**** 來定義及使用自訂色彩。  
  
-   當您在 [物件總管]**** 窗格內指定伺服器項目的色彩時，該色彩會在開啟 [查詢編輯器] 視窗時使用。 若要開啟 [查詢編輯器] 視窗，請以滑鼠右鍵按一下伺服器項目並選取 [新增查詢]****，或是在 [物件總管]**** 窗格為使用中而且在此伺服器上為焦點所在時，按一下工具列上的 [新增查詢]****。  
  
-   當您在 [已註冊的伺服器]**** 窗格內指定伺服器項目的色彩時，該色彩會在開啟 [查詢編輯器] 視窗時使用。 若要開啟 [查詢編輯器] 視窗，請以滑鼠右鍵按一下伺服器項目並選取 [新增查詢]****，或是在 [已註冊的伺服器]**** 窗格為使用中而且在此伺服器上為焦點所在時，按一下工具列上的 [新增查詢]****。  
  
-   在 [檔案]**** 功能表上，當您按一下 [新增]**** 然後按一下 [Database Engine 查詢]**** 時，您在 [連接到伺服器]**** 對話方塊內指定的色彩會套用到 [查詢編輯器] 視窗。  
  
 **全部重設**  
 將所有手動輸入的連接屬性值取代成預設值。  
  
 **連線**  
 使用列出的值嘗試進行連接。  
  
 **選項**  
 按一下即可變更對話方塊，並隱藏其他伺服器連接選項，例如記住密碼。  
  
 **測驗**  
 在 [已註冊的伺服器][!INCLUDE[ssDE](../../includes/ssde-md.md)]** 中註冊 ** 時，請按一下以測試連接。  
  
 **另**  
 儲存 [已註冊的伺服器]**** 中的設定。  
  
## <a name="see-also"></a>另請參閱  
 [連接屬性對話方塊](../../database-engine/connection-properties-dialog-box.md)  
  
  
