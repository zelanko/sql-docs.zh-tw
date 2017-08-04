---
title: "將資料庫移轉至 SQL Server on Linux |Microsoft 文件"
description: "本主題說明不同的選項，將資料庫移轉和資料至 SQL Server on Linux。"
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 1619489d-377a-4f32-8930-d4f536539689
ms.custom: H1Hack27Feb2017
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 61b4ba948df071768380d4a6f2b4ddc4421692d8
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="migrate-databases-and-structured-data-to-sql-server-on-linux"></a>將資料庫和結構化的資料移轉到 SQL Server on Linux 

您可以將您的資料庫和資料移轉至 SQL Server 2017 RC2 在 Linux 上執行。 您選擇使用的方法取決於來源資料和您的特定案例。 下列各節提供各種不同的移轉案例的最佳作法。

## <a name="migrate-from-sql-server-on-windows"></a>從 Windows 上的 SQL Server 移轉
如果您想要在 Windows 上的 SQL Server 資料庫移轉到在 Linux 上的 SQL Server 2017，建議使用的技巧是使用 SQL Server 備份和還原。

1. 在 Windows 電腦上建立資料庫的備份。
2. 備份的檔案傳輸至目標 SQL Server Linux 電腦。
3. 將 Linux 電腦上的備份還原。 

如需移轉使用備份與還原資料庫的教學課程，請參閱下列主題：

- [從 Windows 的 SQL Server 資料庫還原至 Linux](sql-server-linux-migrate-restore-database.md)。

它也可將您的資料庫匯出到 BACPAC 檔案 （包含您的資料庫結構描述和資料的壓縮檔案）。 如果您有 BACPAC 檔案，可以將此檔案傳送到 Linux 機器，並將它匯入 SQL Server。 如需詳細資訊，請參閱下列主題：

- [匯出和匯入具有 SSMS 或 SqlPackage.exe 的資料庫](sql-server-linux-migrate-ssms.md)

## <a name="migrate-from-other-database-servers"></a>從其他資料庫伺服器移轉
您可以將其他資料庫系統上的資料庫移轉至在 Linux 上的 SQL Server 2017。 這包括 Microsoft Access、 DB2、 MySQL、 Oracle 和 Sybase 資料庫。 在此案例中，使用 SQL Server 管理小幫手 (SSMA)，自動移轉至 SQL Server on Linux。 如需詳細資訊，請參閱[使用將資料庫移轉到 SQL Server on Linux 的 SSMA](sql-server-linux-migrate-ssma.md)。  

## <a name="migrate-structured-data"></a>將結構化的資料移轉
也有一些技術來匯入的原始資料。 您可能會建構從其他資料庫或資料來源所匯出的資料檔案。 在此情況下，您可以使用 bcp 工具來大量插入資料。 或者，您可以在 Linux 上的 SQL Server 資料庫將資料匯入的 Windows 上執行 SQL Server Integration Services。 SQL Server Integration Services 可讓您匯入期間，在資料上執行更複雜的轉換。 

如需有關這些技術的詳細資訊，請參閱下列主題：

- [使用 bcp 大量複製資料](sql-server-linux-migrate-bcp.md)
- [擷取、 轉換和載入資料的 SQL Server on Linux 與 SSIS](sql-server-linux-migrate-ssis.md) 

