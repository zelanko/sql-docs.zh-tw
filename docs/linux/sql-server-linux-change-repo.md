---
title: "一般可用性的儲存機制註冊 SQL Server on Linux |Microsoft 文件"
description: "將儲存機制從預覽 SQL Server 2017 儲存機制變更為在 Linux 上的通用版本上市 (GA) 儲存機制 （GA 有時也稱為 RTM）。"
author: annashres
ms.author: anshrest
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: Inactive
ms.openlocfilehash: 28c5668598c5464c893c1bf62c19699282ecf7b3
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2018
---
# <a name="change-repositories-from-the-preview-repository-to-the-ga-repository"></a>變更 GA 儲存機制預覽儲存機制從儲存機制

當您升級 SQL Server 2017 從 CTP 2.1、 RC1 或 RC2 通用版本上市 (GA) 版本，您必須切換儲存機制。 下列各節說明您選擇的儲存機制以及如何進行升級前的變更。

## <a name="repository-choices"></a>儲存機制的選擇

請務必注意，有兩種類型的儲存機制的每個散發：

  > [!IMPORTANT]
  > 任何 CTP 2.1 之前的版本必須升級為至少 2.1，然後再升級至 GA

- **累計更新 (CU)**: 累計更新 (CU) 儲存機制自該版本包含基底的 SQL Server 版本和 bug 修正或改進的封裝。 累計更新的發行版本，例如 SQL Server 2017 特有。 它們會以一般的步調發行。

- **GDR**: GDR 儲存機制 含有該發行以來的基底的 SQL Server 版本和僅重大修正程式和安全性更新的封裝。 這些更新也會新增到下一個 CU 版本。

每個 CU 和 GDR 版本包含完整的 SQL Server 封裝和所有先前的更新，該儲存機制。 從 GDR 發行更新至目前的版本支援適用於 SQL Server 變更設定的儲存機制。 您也可以[降級](sql-server-linux-setup.md#rollback)至您的主要版本內任何發佈 (例如： 2017年)。

> [!NOTE]
> 您可以更新從 GDR 發行 CU 釋放隨時藉由變更儲存機制。 更新不支援從 CU GDR 發行的版本。 

## <a name="change-to-a-ga-repository"></a>變更至 GA 儲存機制

若要變更一個來源儲存機制 （CU 或 GDR） 預覽儲存機制，請使用下列步驟：

1. 移除先前設定的預覽儲存機制。

   | 平台 | 儲存機制移除命令 |
   |-----|-----|
   | RHEL | `sudo rm -rf /etc/yum.repos.d/mssql-server.repo` |
   | SLES | `sudo zypper removerepo 'packages-microsoft-com-mssql-server'` |
   | Ubuntu | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server xenial main'` |

1. 如**Ubuntu 只**，匯入公用儲存機制 GPG 索引鍵。

   ```bash
   sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. 設定新的儲存機制。

   | 平台 | Repository | Command |
   |-----|-----|-----|
   | RHEL | CU | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo` |
   | RHEL | GDR | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017-gdr.repo` |
   | SLES | CU  | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo` |
   | SLES | GDR | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017-gdr.repo` |
   | Ubuntu | CU | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)" && sudo apt-get update` |
   | Ubuntu | GDR | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017-gdr.list)" && sudo apt-get update` |

1. [安裝](sql-server-linux-setup.md#platforms)或[更新](sql-server-linux-setup.md#upgrade)使用 GA 儲存機制的 SQL Server。

   > [!IMPORTANT]
   > 此時，如果您選擇執行完整安裝使用[快速入門教學課程](#platforms)，請記住您剛才設定的目標儲存機制。 教學課程中不重複該步驟。 特別是如果您設定的 GDR 儲存機制，因為快速入門教學課程會使用目前的儲存機制。

## <a name="next-steps"></a>後續的步驟

如需有關如何在 Linux 上安裝 SQL Server 2017 的詳細資訊，請參閱[SQL Server on Linux 的安裝指南](sql-server-linux-setup.md)。
