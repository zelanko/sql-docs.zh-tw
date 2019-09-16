---
title: 教學課程：Azure 儲存體服務中 SQL Server 資料檔案 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: e69be67d-da1c-41ae-8c9a-6b12c8c2fb61
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a15f6735ef0ef79b7eb953445c926f60f6bfb12e
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176082"
---
# <a name="tutorial-sql-server-data-files-in-azure-storage-service"></a>教學課程：Azure 儲存體服務中 SQL Server 資料檔案
  歡迎使用 Azure 儲存體服務中的 SQL Server 資料檔案教學課程。 本教學課程可協助您瞭解如何直接將 SQL Server 資料檔案儲存在 Azure Blob 儲存體服務中。  
  
 Azure Blob 儲存體服務的 SQL Server 整合支援是 SQL Server 2014 增強功能。 如需使用這項功能的功能和優點的總覽, 請參閱[在 Azure 中 SQL Server 資料檔案](databases/sql-server-data-files-in-microsoft-azure.md)。  
  
## <a name="what-you-will-learn"></a>學習內容  
 本教學課程示範如何在多個課程中, 將 SQL Server 資料檔案儲存在 Azure 儲存體服務中。 每一課都會將重點放在特定工作上。 首先, 您將瞭解如何在 Azure 中建立儲存體帳戶和容器。 然後, 您將瞭解如何建立 SQL Server 認證, 以便整合 SQL Server 與 Azure 儲存體。 然後, 您將直接在 Azure 儲存體中建立資料庫。 此外，本教學課程會示範加密、移轉以及備份與還原案例。  
  
 本教學課程分成九個課程：  
  
 **[第1課:建立 Azure 儲存體帳戶和容器](../tutorials/lesson-1-create-windows-azure-storage-account-and-container.md)**  
 在這一課, 您會建立 Azure 儲存體帳戶和容器。  
  
 **[第2課。在容器上建立原則並產生共用存取簽章&#40;SAS&#41;金鑰](lesson-1-create-stored-access-policy-and-shared-access-signature.md)**  
 在這一課，您會在 Blob 容器上建立原則以及產生共用存取簽章。  
  
 **[第3課:建立 SQL Server 認證](lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)**  
 在這一課，您會建立認證以儲存用來存取 Azure 儲存體帳戶的安全性資訊。  
  
 **[第4課:在 Azure 儲存體中建立資料庫](../relational-databases/lesson-3-database-backup-to-url.md)**  
 在這一課, 您會使用 [建立資料庫檔案名] 選項, 在 Azure 儲存體中建立資料庫。  
  
 **[第5課:&#40;選擇性&#41;使用 TDE 加密您的資料庫](../relational-databases/lesson-4-restore-database-to-virtual-machine-from-url.md)**  
 在這一課，您會使用透明資料加密 (TDE) 和伺服器憑證來加密資料庫。  
  
 **[第6課:將資料庫從內部部署的來源機器遷移至 Azure 中的目的地機器](lesson-5-backup-database-using-file-snapshot-backup.md)**  
 在這一課, 您會使用 CREATE DATABASE FOR ATTACH 選項, 將資料庫從內部部署遷移至 Azure 中的虛擬機器。  
  
 **[第7課:將資料檔案移至 Azure 儲存體](../relational-databases/lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup.md)**  
 在這一課, 您會使用 ALTER DATABASE 語句, 將資料檔案移至 Azure 儲存體。  
  
 **[第 8 課：將資料庫還原至 Azure 儲存體](../relational-databases/lesson-7-restore-a-database-to-a-point-in-time.md)**  
 在這一課, 您會使用 [還原資料庫] 移動選項, 將資料庫還原到 Azure 儲存體。  
  
 **[第9課:從 Azure 儲存體還原資料庫](lesson-8-restore-as-new-database-from-log-backup.md)**  
 在這一課, 您會使用 [還原資料庫] [移動] 選項, 從 Azure 儲存體還原資料庫。  
  
## <a name="see-also"></a>另請參閱  
 [在 Azure 中 SQL Server 資料檔案](databases/sql-server-data-files-in-microsoft-azure.md)  
  
  
