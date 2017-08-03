---
title: "從物件總管連接到執行個體 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9803a8a0-a8f1-4b65-87b8-989b06850194
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 53043981ec7d3d66f3a16252a5dd90a9ad323aa6
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-an-instance-from-object-explorer"></a>從物件總管連接到執行個體
若要使用物件總管管理物件，您必須先將物件總管連接到包含物件的執行個體。 您可以同時將物件總管連接到多個執行個體。  
  
## <a name="connecting-object-explorer-to-a-server"></a>將物件總管連接到伺服器  
若要使用物件總管，您必須先連接到伺服器。 請在物件總管工具列上，按一下 [連接]，再從下拉式清單中選取伺服器類型。 [連接到伺服器] 對話方塊隨即開啟。 若要連接，您至少必須先提供伺服器名稱以及正確的驗證資訊。  
  
## <a name="optional-object-explorer-connection-settings"></a>選擇性的物件總管連接設定  
當連接到伺服器時，您可以在 [連接到伺服器] 對話方塊中，指定其他連接資訊。 [連接到伺服器] 對話方塊會保留上次使用的設定，新的連接 (例如新的程式碼編輯器視窗) 將會使用這些設定。  
  
若要指定選擇性的連接設定，請遵照下列步驟：  
  
1.  在物件總管工具列上，按一下 [連接]，再按一下要連接的伺服器類型。 此時會出現 **[連接到伺服器]** 對話方塊。  
  
2.  在 [伺服器名稱] 方塊中，輸入您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 執行個體的名稱。  
  
3.  按一下 [選項]。 此時 [連接到伺服器] 對話方塊會顯示其他選項。  
  
4.  按一下 [連接屬性] 索引標籤來設定其他設定。 可用的設定會隨著伺服器類型而不同。 [!INCLUDE[ssDE](../../includes/ssde_md.md)]可以使用下列設定。  
  
    |設定|說明|  
    |-----------|---------------|  
    |**連接到資料庫**|從伺服器的可用資料庫中進行選擇。 這份清單只會顯示您有權檢視的資料庫。|  
    |**網路通訊協定**|從 [共用記憶體]、[TCP/IP] 或 [具名管道] 中進行選取。|  
    |**網路封包大小**|以位元組為單位來進行設定。 預設值是 4096 位元組。|  
    |**連接逾時**|以秒為單位來進行設定。 預設值是 15 秒。|  
    |**執行逾時**|以秒為單位來進行設定。 預設值 (0) 表示執行動作將永不逾時。|  
    |**加密連接**|強制加密。|  
  
5.  若要將指定的伺服器加入已註冊的伺服器清單中，請按一下 [已註冊的伺服器] 索引標籤，按一下新伺服器將出現的位置，再完成連接。  
  
> [!NOTE]  
> 使用 [其他連接參數] 頁面可將更多連接參數新增到連接字串。 如需詳細資訊，請參閱[連接到伺服器 &#40;其他連接參數頁面&#41;](../../ssms/f1-help/connect-to-server-additional-connection-parameters-page.md)。  
  

