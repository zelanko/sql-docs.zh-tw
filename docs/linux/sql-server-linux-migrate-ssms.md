---
title: 匯出和匯入 Linux 上的資料庫 |Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 2210cfc3-c23a-4025-a551-625890d6845f
ms.openlocfilehash: 428af4498fc45a32909e424aecc99b8f6fc3aadb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66705272"
---
# <a name="export-and-import-a-database-on-linux-with-ssms-or-sqlpackageexe-on-windows"></a>匯出和匯入使用 SSMS 或 SqlPackage.exe 在 Windows 上的 Linux 上的資料庫

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

這篇文章示範如何使用[SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)並[SqlPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx)匯出和匯入 SQL Server on Linux 上的資料庫。 SSMS 和 SqlPackage.exe 是 Windows 應用程式，因此您可以連線到 Linux 上的遠端 SQL Server 執行個體的 Windows 機器時，使用這項技術。

您一定要安裝並使用最新版本的 SQL Server Management Studio (SSMS) 中所述[連接到 SQL Server on Linux 的 Windows 上的 使用 SSMS](sql-server-linux-manage-ssms.md)

> [!NOTE]
> 如果您從一個 SQL Server 執行個體將資料庫移轉至另一個，建議是使用[備份和還原](sql-server-linux-migrate-restore-database.md)。

## <a name="export-a-database-with-ssms"></a>使用 SSMS 將資料庫匯出

1. 輸入啟動 SSMS **Microsoft SQL Server Management Studio**在 Windows 搜尋方塊，，然後按一下 傳統型應用程式。

    ![SQL Server Management Studio](./media/sql-server-linux-manage-ssms/ssms.png) 

2. 連接到您的來源資料庫，在 [物件總管] 中。 來源資料庫可以是內部部署上執行的 Microsoft SQL Server 中或在雲端、 Linux、 Windows 或 Docker 和 Azure SQL Database 或 Azure SQL 資料倉儲上。

3. 以滑鼠右鍵按一下 [物件總管] 中的來源資料庫，指向**任務**，然後按一下**匯出資料層應用程式...**

4. 在匯出精靈 中，按一下**下一步**，然後在**設定**索引標籤上，設定 「 匯出至本機磁碟位置或 Azure blob 儲存 BACPAC 檔案。

5. 根據預設，會匯出資料庫中的所有物件。 按一下 [**進階] 索引標籤**並選擇您想要匯出的資料庫物件。

6. 按一下 [下一步]  ，然後按一下 [完成]  。

*。在您選擇的位置成功建立 BACPAC 檔案，您已準備好匯入目標資料庫。

## <a name="import-a-database-with-ssms"></a>使用 SSMS 的資料庫匯入

1. 輸入啟動 SSMS **Microsoft SQL Server Management Studio**在 Windows 搜尋方塊，，然後按一下 傳統型應用程式。

    ![SQL Server Management Studio](./media/sql-server-linux-manage-ssms/ssms.png) 

2. 連接到您的目標伺服器，在 [物件總管] 中。 目標伺服器可以是 Microsoft SQL Server 執行於內部部署或雲端，在 Linux、 Windows 或 Docker 和 Azure SQL Database 或 Azure SQL 資料倉儲中。

3. 以滑鼠右鍵按一下**資料庫**資料夾中 [物件總管]，然後按一下**匯入資料層應用程式...**

4. 若要建立您的目標伺服器的資料庫，指定 BACPAC 檔案從本機磁碟，或選取 Azure 儲存體帳戶和容器上傳 BACPAC 檔案。

5. 提供新資料庫的資料庫名稱。 如果您要匯入 Azure SQL Database 上的資料庫，設定 Microsoft Azure SQL Database 的版本 （服務層）、 資料庫大小上限，以及服務目標 （效能層級）。

6. 按一下 **下一步**，然後按一下**完成**BACPAC 檔案匯入您的目標伺服器中的新資料庫。

*。在您指定的目標伺服器中建立新的資料庫匯入 BACPAC 檔案。

## <a id="sqlpackage"></a> SqlPackage 命令列選項

您也可使用 SQL Server Data Tools (SSDT) 的命令列工具， [SqlPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx)，以匯出和匯入 BACPAC 檔案。

下列範例命令會匯出 BACPAC 檔案：

```bash
SqlPackage.exe /a:Export /ssn:tcp:<your_server> /sdn:<your_database> /su:<username> /sp:<password> /tf:<path_to_bacpac>
```

使用下列命令來匯入資料庫結構描述和使用者資料。BACPAC 檔案：

```bash
SqlPackage.exe /a:Import /tsn:tcp:<your_server> /tdn:<your_database> /tu:<username> /tp:<password> /sf:<path_to_bacpac>

```

## <a name="see-also"></a>另請參閱
如需有關如何使用 SSMS 的詳細資訊，請參閱 <<c0> [ 使用 SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx)。 如需有關 SqlPackage.exe 的詳細資訊，請參閱[SqlPackage 的參考文件](https://msdn.microsoft.com/library/hh550080.aspx)。
