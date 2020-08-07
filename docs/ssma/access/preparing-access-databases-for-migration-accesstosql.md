---
title: 準備 Access 資料庫以進行遷移 (AccessToSQL) |Microsoft Docs
description: 瞭解如何判斷要遷移哪些 Access 資料庫來 SQL Server 或 Azure SQL Database，並確定這些資料庫已準備好進行遷移。
ms.prod: sql
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases, versions
- Access databases, when to migrate
- Access databases, workgroup security
- backing up databases
- documenting databases
- files, preparing
- migrating databases, versions
- migrating databases, when to migrate
- versions of Access
- workgroup security
ms.assetid: 9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 038ffa60562a443c916d0143fa432d3e5da87bc4
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87937793"
---
# <a name="preparing-access-databases-for-migration-accesstosql"></a>準備 Access 資料庫以進行遷移 (AccessToSQL) 
將 Access 資料庫移轉至之前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，您必須先決定要遷移的資料庫，並確保這些資料庫已準備好進行遷移。  
  
## <a name="determining-when-to-migrate-to-sql-server"></a>判斷遷移至 SQL Server 的時機  
Jet 資料庫引擎是用來做為 Access 的資料庫引擎，它是一種彈性且容易使用的資料管理解決方案。 不過，隨著資料庫變得更大且任務關鍵性，許多使用者發現它們需要更高的效能、安全性或可用性。 針對需要更健全之資料平臺的應用程式，請考慮將這些應用程式的基礎資料庫移至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如需決定何時要遷移的詳細資訊，請參閱網站上的 [[遷移資訊] 頁面](https://go.microsoft.com/fwlink/?LinkId=68571) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
在您將資料庫移轉到之後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，您可以繼續使用連結資料表的存取權，也可以手動將應用程式遷移至 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 直接與互動的 .NET Framework 型程式 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代碼。  
  
## <a name="determining-which-databases-to-migrate"></a>判斷要遷移的資料庫  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]移轉小幫手 (SSMA) 以取得存取權，可以為您找到 Access 資料庫。 接著，您可以將這些資料庫的相關中繼資料匯出至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如需如何匯出和查詢中繼資料的詳細資訊，請參閱[匯出存取清查](exporting-an-access-inventory-accesstosql.md)。  

   > [!NOTE]
   > 並非所有存取功能和設定都受到的支援，或者可以輕鬆地轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 在您開始遷移資料庫之前，請參閱[不相容的存取功能](incompatible-access-features-accesstosql.md)。
  
## <a name="preparing-for-migration"></a>準備進行移轉  
使用下列指導方針來協助您準備存取資料庫，以便遷移至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
### <a name="upgrading-older-access-databases"></a>升級較舊的 Access 資料庫  
SSMA for Access 支援 Access 97 和更新版本。 如果您有舊版 Access 的資料庫，請開啟並將資料庫儲存在 Access 97 或更新版本中。  
  
### <a name="removing-workgroup-protection"></a>正在移除工作組保護  
SSMA 無法遷移使用工作組保護的資料庫。 若要從 Access 資料庫中移除工作組保護，請執行下列步驟：  
  
1.  將 Access 資料庫檔案複製到另一個位置。  
  
2.  開啟複製的資料庫。  
  
3.  在 [**工具**] 功能表上，指向 [**安全性**]，然後選取 [**使用者和群組許可權**]。  
  
4.  選取 [**使用者**] 選項，選取 [系統**管理員**] 使用者，然後確定已選取 [**管理**] 許可權。  
  
5.  選取 [**群組**] 選項，選取 [**使用者**] 群組，然後確定已選取 [**管理**] 許可權。  
  
6.  按一下 **[確定]**，**然後在 [** 檔案] 功能表**Exit**上，按一下 [結束]。  
  
您現在可以使用 SSMA 來遷移已複製的資料庫。 將架構載入至之後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，您可以在上手動保護資料庫 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
### <a name="backing-up-databases"></a>備份資料庫  
將 Access 資料庫移轉至之前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，您應該備份要遷移的 access 資料庫，以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 您將在其中遷移存取物件和資料的資料庫。  
  
若要備份 Access 資料庫，請在 [**工具**] 功能表上，指向 [**資料庫公用程式**]，然後選取 [**備份資料庫**]。  
  
如需有關如何備份資料庫的詳細資訊 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請參閱《 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的「備份和還原資料庫」 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
### <a name="documenting-databases"></a>記錄資料庫  
您可能也會想要記載 Access 資料庫的屬性，例如資料庫物件清單、檔案大小和許可權。 若要在 [存取] 中產生此檔，請在 [**工具**] 功能表上指向 [**分析**]，然後按一下 [**記載**的]。  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[將存取應用程式連結至 SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)
