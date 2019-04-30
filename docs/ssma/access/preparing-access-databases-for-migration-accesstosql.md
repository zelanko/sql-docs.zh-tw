---
title: 準備 Access 資料庫的移轉 (AccessToSQL) |Microsoft Docs
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
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: 9495ff7a58da124255cc6bf5674d92ebeef4c2b0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63299483"
---
# <a name="preparing-access-databases-for-migration-accesstosql"></a>準備 Access 資料庫的移轉 (AccessToSQL)
移轉至 Access 資料庫之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您必須判斷哪些資料庫移轉，並確保這些資料庫準備好進行移轉。  
  
## <a name="determining-when-to-migrate-to-sql-server"></a>判斷何時要移轉至 SQL Server  
Jet 資料庫引擎，用來作為資料庫引擎進行存取，是有彈性、 簡單易用的解決方案，適用於資料管理。 不過，隨著變得越來越大的資料庫及更多的任務關鍵性，許多使用者發現，它們需要較高的效能、 安全性或可用性。 對於需要更強固的資料平台的應用程式，請考慮將應用程式所需的基礎資料庫移[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需有關如何決定何時要移轉的詳細資訊，請參閱 <<c0> [ 移轉資訊頁面](https://go.microsoft.com/fwlink/?LinkId=68571)上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]網站。  
  
您將資料庫移轉至之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您可以繼續使用存取是透過連結的資料表，或您可以手動將移轉您的應用程式[!INCLUDE[msCoName](../../includes/msconame_md.md)].NET Framework 為基礎的程式碼直接互動[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="determining-which-databases-to-migrate"></a>判斷哪一個要移轉的資料庫  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 移轉小幫手 (SSMA) 的存取可以讓您找到 Access 資料庫。 您接著可以將匯出到這些資料庫的相關中繼資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需如何匯出及查詢中繼資料的詳細資訊，請參閱[匯出 Access 清查](exporting-an-access-inventory-accesstosql.md)。  

   > [!NOTE]
   > 並非所有的存取功能和設定支援，或可以輕鬆地轉換成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 在開始移轉資料庫之前，請參閱[不相容的存取功能](incompatible-access-features-accesstosql.md)。
  
## <a name="preparing-for-migration"></a>準備移轉  
使用下列指導方針以協助準備您的 Access 資料庫移轉到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
### <a name="upgrading-older-access-databases"></a>升級舊版的 Access 資料庫  
SSMA for Access 支援 Access 97 和更新版本。 如果您的資料庫從舊版的存取權，開啟，並將資料庫儲存在 Access 97 或更新版本。  
  
### <a name="removing-workgroup-protection"></a>工作群組中移除保護  
SSMA 無法移轉使用工作群組保護的資料庫。 若要從 Access 資料庫中移除工作群組的保護，請執行下列步驟：  
  
1.  將 Access 資料庫檔案複製到另一個位置。  
  
2.  開啟已複製的資料庫。  
  
3.  在 **工具**功能表上，指向**安全性**，然後選取**使用者和群組權限**。  
  
4.  選取**使用者**選項中，選取**Admin**使用者，然後確定**管理**選取權限。  
  
5.  選取 **群組**選項中，選取**使用者**分組，並確定該**管理**選取權限。  
  
6.  按一下  **確定**，然後在**檔案**功能表上，按一下 **結束**。  
  
您現在可以使用 SSMA 移轉已複製的資料庫。 載入結構描述讀入之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您可以手動將資料庫保護上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
### <a name="backing-up-databases"></a>備份資料庫  
您要將 Access 資料庫移轉之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您應該備份這兩個將移轉的 Access 資料庫，以及[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]將您移轉的資料庫存取物件和資料。  
  
若要將 Access 資料庫進行備份上**工具**功能表上，指向**資料庫公用程式**，然後選取**備份資料庫**。  
  
如需有關如何備份資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫，請參閱 「 備份和還原的資料庫中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]"在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]線上叢書 》。  
  
### <a name="documenting-databases"></a>文件資料庫  
您也可以在文件的屬性，例如資料庫物件、 檔案大小和存取資料庫的權限的清單。 若要產生在 Access 中，這份文件上**工具**功能表上，指向**分析**，然後按一下**記載**。  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[連結到 SQL Server 的 Access 應用程式](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)
