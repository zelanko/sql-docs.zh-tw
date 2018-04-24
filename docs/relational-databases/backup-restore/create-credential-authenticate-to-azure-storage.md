---
title: 建立認證 - 向 Azure 儲存體驗證 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.backuptourl.createcred.f1
ms.assetid: 0622619d-27c5-4ff0-83e5-cde31648c27a
caps.latest.revision: 7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2227e361efc83c16dbfc3c76e75af5ef5fdb208a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="create-credential---authenticate-to-azure-storage"></a>建立認證 - 向 Azure 儲存體驗證
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  使用 **[備份至 URL - 建立認證]** 對話方塊建立新的 SQL 認證。  
  
 使用此對話方塊建立認證時，您必須提供新增至本機憑證存放區的 Windows Azure 管理憑證或下載到電腦上的發行設定檔，以驗證訂閱和儲存體帳戶資訊。  
  
 **SQL 認證**  
 指定您要建立之 SQL 認證的名稱。  
  
## <a name="windows-azure-credentials"></a>Windows Azure 認證  
 **管理憑證**  
 使用這個選項可從本機憑證存放區指定憑證，該憑證符合 Windows Azure 中的管理憑證。 如需 Windows Azure 管理憑證的詳細資訊，請參閱＜ [建立及上傳 Windows Azure 的管理憑證](http://go.microsoft.com/fwlink/?LinkId=320781)＞。  
  
 **訂閱**  
 選取、輸入或貼上符合本機憑證存放區之管理憑證的 Windows Azure 訂閱識別碼。  
  
 **發行設定檔**  
 如果您擁有下載到電腦上的發行設定檔，請使用這個選項。 如果您使用這個選項，則會自動填入訂閱識別碼和憑證。  
  
> [!CAUTION]  
>  SQL Server 目前支援發行設定檔 2.0 版。 若要下載發行設定檔的支援版本，請參閱＜ [下載發行設定檔 2.0](http://go.microsoft.com/fwlink/?LinkId=396421)＞。  
  
## <a name="storage-account"></a>儲存體帳戶  
 選取您想要用來儲存備份檔案的儲存體帳戶。  
  
  
