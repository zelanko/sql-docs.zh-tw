---
title: 將資料庫移轉至 Linux 上的 SQL Server |Microsoft Docs
description: 本文說明在 Linux 上的移轉的資料庫和資料到 SQL Server 的不同選項。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.technology: linux
ms.assetid: 1619489d-377a-4f32-8930-d4f536539689
ms.custom: sql-linux
ms.openlocfilehash: 818920fe2f79a19253f2a0a943a77fe0c067df1f
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39083661"
---
# <a name="migrate-databases-and-structured-data-to-sql-server-on-linux"></a>將資料庫和結構化的資料移轉至 Linux 上的 SQL Server 

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

您可以將您的資料庫和資料移轉至在 Linux 上執行的 SQL Server 2017。 您選擇使用的方法取決於來源資料和您的特定案例。 下列各節提供各種不同的移轉案例的最佳作法。

## <a name="migrate-from-sql-server-on-windows"></a>從 Windows 上的 SQL Server 移轉
如果您想要在 Windows 上的 SQL Server 資料庫移轉至 Linux 上的 SQL Server 2017 時，建議的技巧是使用 SQL Server 備份和還原。

1. 在 Windows 電腦上建立資料庫的備份。
2. 將備份的檔案傳輸至目標 SQL Server Linux 機器。
3. 在 Linux 機器上的備份還原。 

如需使用備份與還原將資料庫移轉的教學課程，請參閱下列主題：

- [從 Windows 的 SQL Server 資料庫還原到 Linux](sql-server-linux-migrate-restore-database.md)。

它也可將您的資料庫匯出到 BACPAC 檔案 （包含您的資料庫結構描述和資料壓縮檔案）。 如果您有 BACPAC 檔案，您可以將此檔案傳送到您的 Linux 機器，並再將它匯入至 SQL Server。 如需詳細資訊，請參閱下列主題：

- [匯出和匯入使用 SSMS 或 SqlPackage.exe 的資料庫](sql-server-linux-migrate-ssms.md)

## <a name="migrate-from-other-database-servers"></a>從其他資料庫伺服器移轉
您可以將其他資料庫系統上的資料庫移轉至 Linux 上的 SQL Server 2017。 這包括 Microsoft Access、 DB2、 MySQL、 Oracle 及 Sybase 資料庫。 在此案例中，使用 SQL Server 管理小幫手 (SSMA) 自動移轉至 Linux 上的 SQL Server。 如需詳細資訊，請參閱 < [，將資料庫移轉到 Linux 上的 SQL Server 使用 SSMA](sql-server-linux-migrate-ssma.md)。  

## <a name="migrate-structured-data"></a>移轉的結構化的資料
另外還有匯入未經處理資料的技術。 您可能會有結構化資料從其他資料庫或資料來源所匯出的檔案。 在此情況下，您可以使用 bcp 工具來大量插入資料。 或者，您可以在 Linux 上的 SQL Server 資料庫將資料匯入的 Windows 上執行 SQL Server Integration Services。 SQL Server Integration Services 可讓您在匯入期間對資料執行更複雜的轉換。 

如需有關這些技術的詳細資訊，請參閱下列主題：

- [使用 bcp 大量複製資料](sql-server-linux-migrate-bcp.md)
- [擷取、 轉換和載入資料，使用 SSIS 在 Linux 上的 SQL server](sql-server-linux-migrate-ssis.md) 
