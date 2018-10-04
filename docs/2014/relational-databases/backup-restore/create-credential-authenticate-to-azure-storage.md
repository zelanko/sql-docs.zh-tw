---
title: 建立認證 - 向 Azure 儲存體驗證 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.backuptourl.createcred.f1
ms.assetid: 0622619d-27c5-4ff0-83e5-cde31648c27a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 62ab149ad9bd20c9c33c416f46ec18b01356fd10
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48204928"
---
# <a name="create-credential---authenticate-to-azure-storage"></a>建立認證 - 向 Azure 儲存體驗證
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
  
  
