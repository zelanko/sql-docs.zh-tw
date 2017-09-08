---
title: "準備移轉 (AccessToSQL) 的 Access 資料庫 |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 08/15/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
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
caps.latest.revision: 20
author: Shamikg
ms.author: Shamikg
manager: murato
ms.translationtype: MT
ms.sourcegitcommit: e4a6157cb56c6db911406585f841046a431eef99
ms.openlocfilehash: 0d94578759156dcde898a23267fb91922fc98b03
ms.contentlocale: zh-tw
ms.lasthandoff: 08/16/2017

---
# <a name="preparing-access-databases-for-migration-accesstosql"></a>準備移轉 (AccessToSQL) 的 Access 資料庫
移轉至 Access 資料庫之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，您必須判斷哪些資料庫移轉，並確保這些資料庫準備好進行移轉。  
  
## <a name="determining-when-to-migrate-to-sql-server"></a>判斷要移轉到 SQL Server 的時機  
Jet 資料庫引擎，可做為資料庫引擎的存取，是資料管理的彈性且容易使用解決方案。 不過，做為資料庫變得越來越大和多個非常關鍵，許多使用者發現需要更高的效能、 安全性或可用性。 對於需要更強固的資料平台的應用程式，請考慮將移至這些應用程式的基礎資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 如需決定何時要移轉的詳細資訊，請參閱[移轉資訊頁面](http://go.microsoft.com/fwlink/?LinkId=68571)上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]網站。  
  
移轉資料庫之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]、 您可以繼續使用存取使用連結的資料表，或您可以手動將移轉您的應用程式[!INCLUDE[msCoName](../../includes/msconame_md.md)].NET Framework 為基礎的程式碼直接互動[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
## <a name="determining-which-databases-to-migrate"></a>判斷哪一個要移轉的資料庫  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]移轉小幫手 (SSMA) 的存取可以找到您的 Access 資料庫。 然後，您可以匯出至這些資料庫的相關中繼資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 如需如何匯出和查詢中繼資料的詳細資訊，請參閱[匯出存取清查](http://msdn.microsoft.com/7e1941fb-3d14-4265-aff6-c77a4026d0ed)。  

   > [!NOTE]
   > 並非所有的存取功能和設定或不支援，可以輕鬆地轉換成[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 在開始移轉資料庫之前，請參閱[不相容的存取功能](http://msdn.microsoft.com/99d45b9c-e3b9-4d56-8c25-b594b887ace1)。
  
## <a name="preparing-for-migration"></a>準備移轉  
使用下列指導方針可協助您準備移轉到 Access 資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
### <a name="upgrading-older-access-databases"></a>升級舊版的 Access 資料庫  
SSMA for Access 支援 Access 97 和更新版本。 如果您的資料庫從舊版的存取權，開啟，並將資料庫儲存在 Access 97 或更新版本。  
  
### <a name="removing-workgroup-protection"></a>移除工作群組的保護  
SSMA 無法移轉使用工作群組保護的資料庫。 若要從 Access 資料庫中移除工作群組的保護，請執行下列步驟：  
  
1.  將 Access 資料庫檔案複製到另一個位置。  
  
2.  開啟已複製的資料庫。  
  
3.  在**工具**功能表上，指向**安全性**，然後選取**使用者和群組權限**。  
  
4.  選取**使用者**選項中，選取**Admin**使用者，然後確定**管理**選取權限。  
  
5.  選取**群組**選項中，選取**使用者**群組，並確定**管理**選取權限。  
  
6.  按一下**確定**，然後在**檔案**功能表上，按一下 **結束**。  
  
您現在可以使用 SSMA 移轉複製的資料庫。 載入至結構描述之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，您可以手動將資料庫安全上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
### <a name="backing-up-databases"></a>備份資料庫  
移轉程式存取資料庫之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，您應該備份這兩個您將移轉的 Access 資料庫，以及[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]您要移轉到其中的資料庫存取物件和資料。  
  
Access 資料庫中，備份上**工具**功能表上，指向**資料庫公用程式**，然後選取**備份資料庫**。  
  
如需有關如何備份資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫，請參閱"Backing Up and Restoring Databases 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]」 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]線上叢書 》。  
  
### <a name="documenting-databases"></a>記錄資料庫  
您也可以在文件的屬性，例如資料庫物件、 檔案大小、 及權限，存取資料庫的清單。 若要產生在 Access 中，這份文件上**工具**功能表上，指向**分析**，然後按一下  **Documented**。  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](http://msdn.microsoft.com/76a3abcf-2998-4712-9490-fe8d872c89ca)  
[連結到 SQL Server 存取應用程式](http://msdn.microsoft.com/82374ad2-7737-4164-a489-13261ba393d4)
