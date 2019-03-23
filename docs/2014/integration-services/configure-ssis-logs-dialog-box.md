---
title: 設定 SSIS 記錄對話方塊 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.configuredtslogs.loggingdetails.f1
- sql12.dts.designer.configuredtslogs.providersandlogs.f1
- sql12.dts.designer.configuredtslogs.containers.f1
helpviewer_keywords:
- Configure SSIS Logs dialog box
ms.assetid: 4b980275-cd9a-4943-8c36-727d51f9a484
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: dbba1b7712bcbdccc821e419b3101065c3164913
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58375208"
---
# <a name="configure-ssis-logs-dialog-box"></a>設定 SSIS 記錄對話方塊
  使用 **[設定 SSIS 記錄]** 對話方塊定義封裝的記錄選項。  
  
 **您想要做什麼事？**  
  
1.  [開啟 [設定 SSIS 記錄] 對話方塊。](#open_dialog)  
  
2.  [設定 [容器] 窗格中的選項](#container)  
  
3.  [設定 [提供者與記錄] 索引標籤上的選項](#provider)  
  
4.  [設定 [詳細資料] 索引標籤上的選項](#detail)  
  
##  <a name="open_dialog"></a> 開啟 [設定 SSIS 記錄] 對話方塊。  
 **開啟 [設定 SSIS 記錄] 對話方塊**  
  
-   在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師中，按一下 **[SSIS]** 功能表上的 **[記錄]** 。  
  
##  <a name="container"></a> 設定 [容器] 窗格中的選項  
 使用 **[設定 SSIS 記錄]** 對話方塊的 **[容器]** 窗格，即可啟用封裝及其容器以進行記錄。  
  
### <a name="options"></a>選項。  
 **[設定 SSIS 記錄]**  
 在階層式檢視中選取核取方塊，即可啟用封裝及其容器以進行記錄：  
  
-   如果已清除，則表示並未啟用容器來進行記錄。 選取即可啟用記錄。  
  
-   如果呈暗灰色，容器就會使用其父系的記錄選項。 封裝無法使用此選項。  
  
-   如果已核取，則容器會定義它自己的記錄選項。  
  
 如果容器呈暗灰色，而您要在容器上設定記錄選項，請按兩下其核取方塊。 第一次點選時會清除核取方塊，而第二次點選則會選取核取方塊，讓您可以選擇要使用的記錄提供者和選取要記錄的資訊。  
  
##  <a name="provider"></a> 設定 [提供者與記錄] 索引標籤上的選項  
 使用 [設定 SSIS 記錄] 對話方塊的 [提供者與記錄] 索引標籤，即可建立和設定用於擷取執行階段事件的記錄。  
  
### <a name="options"></a>選項。  
 **提供者類型**  
 從清單中選取記錄提供者的類型。  
  
 **[加入]**  
 將所指定類型的記錄加入至封裝之記錄提供者的集合。  
  
 **名稱**  
 使用這些核取方塊，啟用或停用容器的記錄，或是 [設定 SSIS 記錄] 對話方塊的 [容器] 窗格中選取之工作的記錄。 名稱欄位是可編輯的。 使用提供者的預設名稱，或輸入唯一的描述性名稱。  
  
 **說明**  
 描述欄位是可編輯的。 按一下，然後修改記錄的預設描述。  
  
 **Configuration**  
 在清單中選取現有連線管理員，或按一下 [\<新增連線...>]，即可建立新的連線管理員。 視記錄提供者的類型而定，您可以設定 OLE DB 連接管理員或檔案連接管理員。 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 事件記錄檔的記錄提供者不需要有連接。  
  
 相關主題：[OLE DB 連線管理員](connection-manager/ole-db-connection-manager.md)總監[檔案 」 連接管理員](connection-manager/file-connection-manager.md)  
  
 **刪除**  
 選取記錄提供者，然後按一下 [刪除]。  
  
##  <a name="detail"></a> 設定 [詳細資料] 索引標籤上的選項  
 使用 **[設定 SSIS 記錄]** 對話方塊的 **[詳細資料]** 索引標籤，即可指定要啟用記錄的事件以及要記錄的資訊詳細資料。 您選取的資訊適用於封裝中的所有記錄提供者。 例如，您無法寫入部份資訊到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體，而寫入不同資訊到文字檔。  
  
### <a name="options"></a>選項。  
 **事件**  
 啟用或停用記錄事件。  
  
 **說明**  
 檢視事件的描述。  
  
 **進階**  
 選取或清除要記錄的事件，以及選取或清除要為每個事件記錄的資訊。 按一下 **[基本]** ，即可隱藏除了事件清單以外的所有記錄詳細資料。 記錄可以使用下列資訊：  
  
|值|描述|  
|-----------|-----------------|  
|**電腦**|記錄事件發生所在之電腦的名稱。|  
|**運算子**|啟動封裝之人員的使用者名稱。|  
|**SourceName**|記錄事件發生所在之封裝、容器或工作的名稱。|  
|**SourceID**|記錄事件發生所在之封裝、容器或工作的全域唯一識別碼 (GUID)。|  
|**ExecutionID**|封裝執行個體的全域唯一識別碼。|  
|**MessageText**|與記錄項目相關聯的訊息。|  
|**DataBytes**|保留供日後使用。|  
  
 **[基本]**  
 選取或清除要記錄的事件。 此選項會隱藏除了事件清單以外的記錄詳細資料。 依預設，如果您選取某個事件，該事件的所有記錄詳細資料都會被選取。 按一下 **[進階]** ，即可顯示所有的記錄詳細資料。  
  
 **載入**  
 指定現有的 XML 檔案，即可用來作為設定記錄選項的範本。  
  
 **儲存**  
 將組態詳細資料儲存為 XML 檔案的範本。  
  
  
