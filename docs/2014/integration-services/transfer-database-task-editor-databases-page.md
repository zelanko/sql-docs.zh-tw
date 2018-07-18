---
title: 傳送資料庫工作編輯器 （資料庫頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferdatabasetask.database.f1
helpviewer_keywords:
- Transfer Database Task Editor
ms.assetid: ccdb74d0-4bea-420c-a726-2e0eb8957e0a
caps.latest.revision: 24
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 24de303a26a148ffe44b643e10a78c77a1ee4d3d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37231478"
---
# <a name="transfer-database-task-editor-databases-page"></a>傳送資料庫工作編輯器 (資料庫頁面)
  使用 [傳送資料庫工作編輯器] 對話方塊的 [資料庫] 頁面，即可指定傳送資料庫工作中所含之來源和目的地資料庫的屬性。 傳送資料庫工作會在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的兩個執行個體間，複製或移動 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]資料庫。 這項工作也可用來在同一部伺服器內複製資料庫。 如需這項工作的詳細資訊，請參閱 [傳送資料庫工作](control-flow/transfer-database-task.md)。  
  
## <a name="options"></a>選項。  
 **SourceConnection**  
 在清單中選取 SMO 連線管理員，或按一下 [\<新增連線...>] 建立來源伺服器的新連線。  
  
 **DestinationConnection**  
 在清單中選取一個 SMO 連線管理員，或按一下 [\<新增連線...>]，以建立目的地伺服器的新連線。  
  
 **DestinationDatabaseName**  
 指定目的地伺服器上之 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫的名稱。  
  
 若要使用來源資料庫名稱來自動擴展此欄位，請先指定 **SourceConnection** 和 **SourceDatabaseName** 。  
  
 若要重新命名目的地伺服器上的資料庫，請在此欄位中輸入新名稱。  
  
 **DestinationDatabaseFiles**  
 指定目的地伺服器上之資料庫檔案的名稱和位置。  
  
 若要使用來源資料庫檔案的名稱和位置來自動擴展此欄位，請先指定 **SourceConnection**、 **SourceDatabaseName**和 **SourceDatabaseFiles** 。  
  
 若要重新命名資料庫檔案，或要指定目的地伺服器上的新位置，請使用來源資料庫的資訊來擴展此欄位，然後按一下瀏覽按鈕。 在 [目的地資料庫檔案] 對話方塊中，編輯 [目的地檔案]、[目的資料夾] 或 [網路檔案共用]。  
  
> [!NOTE]  
>  如果您是使用瀏覽按鈕找到資料庫檔案，就可以使用本機磁碟機代號來輸入檔案位置：例如 c:\\。 您必須以網路共用標記來取代此檔案位置，其中包含電腦名稱和共用名稱。 如果使用預設管理共用，您就必須使用 $ 標記，並具有管理權限存取該共用。  
  
 **DestinationOverwrite**  
 指定是否可以覆寫目的地伺服器上的資料庫。  
  
 此屬性具有下表所列的選項：  
  
|值|描述|  
|-----------|-----------------|  
|**True**|覆寫目的地伺服器資料庫。|  
|**False**|請勿覆寫目的地伺服器資料庫。|  
  
> [!CAUTION]  
>  如果您為 **DestinationOverwrite** 指定了 **True**，此舉可能會造成資料遺失，且會覆寫目的地伺服器資料庫中的資料。 為了避免此情形發生，在執行傳送資料庫工作之前，請先將目的地伺服器資料庫備份至其他位置。  
  
 **動作**  
 指定工作會將資料庫 [複製] 或 [移動] 至目的地伺服器。  
  
 **方法**  
 指定當來源伺服器上的資料庫處於線上或離線模式時，是否會執行工作。  
  
 若要使用離線模式來傳送資料庫，執行封裝的使用者就必須是 **系統管理員** 固定伺服器角色的成員。  
  
 若要使用線上模式來傳送資料庫，執行封裝的使用者就必須是 **系統管理員** 固定伺服器角色的成員，或是選取之資料庫的資料庫擁有者 (**dbo**)。  
  
 **SourceDatabaseName**  
 選取要複製或移動之資料庫的名稱。  
  
 **SourceDatabaseFiles**  
 按一下瀏覽按鈕，即可選取資料庫檔案。  
  
 **ReattachSourceDatabase**  
 指定失敗發生時，工作是否會嘗試重新附加來源資料庫。  
  
 此屬性具有下表所列的選項：  
  
|值|描述|  
|-----------|-----------------|  
|**True**|重新附加來源資料庫。|  
|**False**|請勿重新附加來源資料庫。|  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Integration Services 工作](control-flow/integration-services-tasks.md)   
 [傳送資料庫工作編輯器&#40;一般頁面&#41;](general-page-of-integration-services-designers-options.md)   
 [運算式頁面](expressions/expressions-page.md)   
 [SMO 連線管理員](connection-manager/smo-connection-manager.md)  
  
  
