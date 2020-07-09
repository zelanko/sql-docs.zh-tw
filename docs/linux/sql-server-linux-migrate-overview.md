---
title: 將資料庫遷移到 Linux 上的 SQL Server
description: 此文章說明將資料庫和資料遷移到 Linux 上的 SQL Server 的不同選項。
author: VanMSFT
ms.author: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1619489d-377a-4f32-8930-d4f536539689
ms.openlocfilehash: 185d62a67309f9e76e5f738494ee2137e2ef4a73
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85897766"
---
# <a name="migrate-databases-and-structured-data-to-sql-server-on-linux"></a>將資料庫和結構化資料遷移到 Linux 上的 SQL Server 

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

您可以將您的資料庫和資料，遷移到在 Linux 上執行的 SQL Server。 您選擇使用的方法取決於來源資料和您的特定案例。 下列小節提供各種移轉案例的最佳做法。

## <a name="migrate-from-sql-server-on-windows"></a>從 Windows 上的 SQL Server 遷移
如果您想要將 Windows 上的 SQL Server 資料庫遷移到 Linux 上的 SQL Server，建議使用的技術是 SQL Server 備份和還原。

1. 在 Windows 機器上建立資料庫的備份。
2. 將備份檔案傳輸至目標 SQL Server Linux 機器。
3. 在 Linux 機器上還原備份。 

如需使用備份和還原來遷移資料庫的教學課程，請參閱下列主題：

- [將 SQL Server 資料庫從 Windows 還原至 Linux](sql-server-linux-migrate-restore-database.md)。

您也可以將資料庫匯出到 BACPAC 檔案 (包含資料庫結構描述和資料的壓縮檔案)。 如果您有 BACPAC 檔案，您可以將此檔案傳輸至 Linux 電腦，然後將它匯入 SQL Server。 如需詳細資訊，請參閱下列主題：

- [使用 SSMS 或 SqlPackage.exe 匯出和匯入資料庫](sql-server-linux-migrate-ssms.md)

## <a name="migrate-from-other-database-servers"></a>從其他資料庫伺服器遷移
您可以將其他資料庫系統上的資料庫遷移到 Linux 上的 SQL Server。 包括 Microsoft Access、DB2、MySQL、Oracle 和 Sybase。 在此案例中，請使用 SQL Server 管理助理 (SSMA) 來自動化遷移到 Linux 上的 SQL Server 的程序。 如需詳細資訊，請參閱[使用 SSMA 將資料庫遷移到 Linux 上的 SQL Server](sql-server-linux-migrate-ssma.md)。  

## <a name="migrate-structured-data"></a>遷移結構化資料
此外，也有匯入原始資料的技術。 您可能有從其他資料庫或資料來源匯出的結構化資料檔案。 在此情況下，您可以使用 bcp 工具來大量插入資料。 或者，您也可以在 Windows 上執行 SQL Server Integration Services，將資料匯入至 Linux 上的 SQL Server 資料庫。 SQL Server Integration Services 可讓您在匯入期間對資料執行更複雜的轉換。 

如需有關這些技術的詳細資訊，請參閱下列主題：

- [使用 bcp 大量複製資料](sql-server-linux-migrate-bcp.md)
- [使用 SSIS 對 Linux 上的 SQL Server 擷取、轉換和載入資料](sql-server-linux-migrate-ssis.md) 
