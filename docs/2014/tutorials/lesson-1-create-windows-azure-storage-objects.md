---
title: 第1課：建立 Azure 儲存體物件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 74edd1fd-ab00-46f7-9e29-7ba3f1a446c5
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 53fcba3401a6798fb865613470ba78aa05e9b6dd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "70176103"
---
# <a name="lesson-1-create-azure-storage-objects"></a>第 1 課：建立 Azure 儲存體物件
  您必須先建立儲存體帳戶，然後建立 Blob 容器，才能在雲端儲存體上建立 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 備份。 第1課會引導您完成登入 Azure 管理入口網站、建立儲存體帳戶和 blob 容器的步驟。  
  
## <a name="create-a-storage-account"></a>建立儲存體帳戶  
 若要從 Azure 管理入口網站建立儲存體帳戶，請使用下列步驟：  
  
1.  使用您的帳戶，登入 Azure 管理入口網站。 如果您沒有 Azure 帳戶，請[造訪 azure 3 個月免費試用](https://go.microsoft.com/fwlink/?LinkId=271927)。  
  
     ![Azure 登入畫面](../../2014/tutorials/media/windowazurelogin-backuptocloud.gif "Azure 登入畫面")  
  
2.  使用[這裡](https://go.microsoft.com/fwlink/?LinkId=271926)詳述的逐步指示來建立儲存體帳戶。  
  
3.  瀏覽至您在上一個步驟中建立的儲存體帳戶。 從網頁的正下方，按一下 [**管理金鑰**]。 帳戶資訊隨即顯示。 複製儲存體帳戶名稱以及存取金鑰。 這項資訊是建立 SQL 預存認證的必要資訊。 
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會使用這項資訊來存取儲存體帳戶並建立備份。  
  
     ![Azure 儲存體帳戶金鑰的螢幕擷取畫面](../../2014/tutorials/media/manageaccesskeys-backuptocloud.gif "Azure 儲存體帳戶金鑰的螢幕擷取畫面")  
  
    > [!NOTE]  
    >  您也可以使用 REST API，以程式設計方式建立儲存體帳戶。 如需詳細資訊，請參閱[建立儲存體帳戶](https://go.microsoft.com/fwlink/?LinkId=271928)。  
  
### <a name="create-a-blob-container"></a>建立 Blob 容器  
 容器可對一組 Blob 進行分組。 所有 Blob 都必須位於容器中。 帳戶可以包含不限數目的容器，但是至少必須具有一個容器。 容器可以儲存無限制的 Blob。  
  
 若要建立容器，請使用下列步驟：  
  
1.  選取儲存體帳戶，按一下 [**容器**] 索引標籤，然後按一下畫面底部的 [**新增容器**]，開啟新的對話方塊。  
  
     ![建立管理入口網站中的容器](../../2014/tutorials/media/backuptocloud.gif "建立管理入口網站中的容器")  
  
2.  輸入容器的名稱。 記下您所指定的容器名稱。 這項資訊會用於第 3 課和第 4 課的 T-SQL 陳述式 URL (備份檔的路徑) 中。  
  
3.  針對 [**存取類型**] 選取 [私用]。 我們建議您建立私用容器以確保備份檔安全。  
  
     ![正在建立新的 BLOB 容器](../../2014/tutorials/media/backuptocloud-newblobcontainer.gif "正在建立新的 BLOB 容器")  
  
    > [!NOTE]  
    >  即使您選擇建立公用容器，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 備份與還原仍然需要儲存體帳戶的驗證。  
    >   
    >  您也可以使用 REST API，以程式設計方式建立容器。 如需詳細資訊，請參閱[Create Container](https://go.microsoft.com/fwlink/?LinkId=271946)。  
  
### <a name="next-lesson"></a>下一課  
 [第2課：建立 SQL Server 認證](../../2014/tutorials/lesson-2-create-a-sql-server-credential.md)。  
  
  
